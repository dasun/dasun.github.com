---
layout: post
title: "Stable Android Orientation Readings"
thumbnail: /images/posts/stable-android-orientation-readings/thumbnail_200x200.png
excerpt: "Most android powered devices have built-in sensors to meassure the orienation of the device. Orientation sensors are capable of providing readings with high precision and accuracy. But the readings obtained directly from these sensors are very unstable and noisy. Here is the technique that I have used to stabilize orientation readings in Android."
tags:
- android
- accelerometer
---
<div style="text-align:justify;">
	<p class="post-image-p">
	<img src="/images/posts/stable-android-orientation-readings/accelerometer.png" class="img-polaroid">
	</p>
<p>
  I am working on an android project again. This time it is 
  a hardware based android project. In the middle of that came into a 
  position where I have to obtain stable orientation readings from the 
  device. In the beginning, I decided to obtain values from the 
  gyroscope and I found the following list of mobile devices contains 
  a built-in gyroscope.
</p>
<h3>
  Phones
</h3>
<ul>
  <li>
    HTC Sensation
  </li>
  <li>
    HTC Sensation XL
  </li>
  <li>
    HTC Evo 3D
  </li>
  <li>
    HTC One S
  </li>
  <li>
    HTC One X
  </li>
  <li>
    Huawei Ascend P1
  </li>
  <li>
    Huawei Ascend X (U9000)
  </li>
  <li>
    Huawei Honor (U8860)
  </li>
  <li>
    LG Nitro HD (P930)
  </li>
  <li>
    LG Optimus 2x (P990)
  </li>
  <li>
    LG 
    Optimus Black (P970)
  </li>
  <li>
    LG Optimus 3D (P920)
  </li>
  <li>
    Samsung 
    Galaxy S II (i9100)
  </li>
  <li>
    Samsung Galaxy S III (i9300)
  </li>
  <li>
    Samsung Galaxy R (i9103)
  </li>
  <li>
    Samsung Google Nexus S (i9020)
  </li>
  <li>
    Samsung Galaxy Nexus (i9250)
  </li>
  <li>
    Samsung Galaxy Note 
    (n7000)
  </li>
  <li>
    Sony Xperia P (LT22i)
  </li>
  <li>
    Sony Xperia S (LT26i)
  </li>
</ul>
<h3>
  Tablets
</h3>
<ul>
  <li>
    Acer Iconia 
    Tab A100 (7&quot;)
  </li>
  <li>
    Acer Iconia Tab A500 (10.1&quot;)
  </li>
  <li>
    Asus Eee Pad Transformer (TF101)
  </li>
  <li>
    Asus Eee Pad Transformer 
    Prime (TF201)
  </li>
  <li>
    Motorola Xoom (mz604)
  </li>
  <li>
    Samsung Galaxy 
    Tab (p1000)
  </li>
  <li>
    Samsung Galaxy Tab 7 plus (p6200)
  </li>
  <li>
    Samsung Galaxy Tab 10.1 (p7100)
  </li>
  <li>
    Sony Tablet P
  </li>
  <li>
    Sony 
    Tablet S
  </li>
  <li>
    Toshiba Thrive 7&quot;
  </li>
  <li>
    Toshiba Trhive 10
    &quot;
  </li>
</ul>
<p>
  But unfortunately none of my devices was 
  in the list. Still the gyroscope is not much popular sensor among 
  android mobile devices. Even though most of the android mobile 
  devices do not have a built-in gyroscope almost all of them have an 
  accelerometer and a magnetometer. So I decided to combine the 
  readings from the accelerometer and magnetometer to obtain 
  orientation data.
</p>
<p>
  With android reading values from 
  these sensors is not a very difficult task except the stabilization 
  of the readings. The reading obtained directly from these sensors 
  are very unstable and noisy. Even when the mobile device is in a 
  stable position I don&#39;t have a stable output. So I realized that 
  to measure actual orientation I have to deal with the noise. I 
  searched all over the internet and could not come up with a complete 
  explanation. But I found some useful information about filters that 
  can be used. 
</p>
<p>
  So I implement a code by using the information 
  about filters.
</p>
</div>

{% highlight java %}
import android.content.Context;
import android.hardware.Sensor;
import android.hardware.SensorEvent;
import android.hardware.SensorEventListener;
import android.hardware.SensorManager;

public class AccelerometerService {
	private static SensorManager sensorManager;
	private static SensorEventListener sensorEventListener;
	private static boolean started = false;

	private static float[] accelerometer = new float[3];
	private static float[] magneticField = new float[3];

	private static float[] rotationMatrix = new float[9];
	private static float[] inclinationMatrix = new float[9];
	private static float[] attitude = new float[3];

	private final static double RAD2DEG = 180 / Math.PI;

	private static int[] attitudeInDegrees = new int[3];
	
	private static final float ALPHA = 0.2f;
	
	//Filter
	public static float[] filter(float[] newValues, float[] previousValues) {
		for(int i = 0; i < newValues.length; i++) {
			previousValues[i] = previousValues[i] + ALPHA * (newValues[i] - previousValues[i]);
		}
		return previousValues;
	}

	public static void start(final Context applicationContext) {
		if (started) {
			return;
		}

		sensorManager = (SensorManager) applicationContext
				.getSystemService(Context.SENSOR_SERVICE);

		sensorEventListener = new SensorEventListener() {

			@Override
			public void onSensorChanged(SensorEvent event) {

				int type = event.sensor.getType();
				if (type == Sensor.TYPE_MAGNETIC_FIELD) {
					magneticField = filter(event.values.clone(), magneticField);
				}
				if (type == Sensor.TYPE_ACCELEROMETER) {
					accelerometer = filter(event.values.clone(), accelerometer);
				}

				SensorManager.getRotationMatrix(rotationMatrix,
						inclinationMatrix, accelerometer, magneticField);
				SensorManager.getOrientation(rotationMatrix, attitude);

				attitudeInDegrees[0] = (int) Math.round(attitude[0] * RAD2DEG);
				attitudeInDegrees[1] = (int) Math.round(attitude[1] * RAD2DEG);
				attitudeInDegrees[2] = (int) Math.round(attitude[2] * RAD2DEG);

			}

			@Override
			public void onAccuracyChanged(Sensor sensor, int accuracy) {

			}
		};
		sensorManager.registerListener(sensorEventListener,
				sensorManager.getDefaultSensor(Sensor.TYPE_ACCELEROMETER),
				SensorManager.SENSOR_DELAY_UI);
		sensorManager.registerListener(sensorEventListener,
				sensorManager.getDefaultSensor(Sensor.TYPE_MAGNETIC_FIELD),
				SensorManager.SENSOR_DELAY_UI);

		started = true;
	}

	public static boolean getStarted() {
		return started;
	}

	public static void stop() {
		if (started) {
			sensorManager.unregisterListener(sensorEventListener);
			started = false;
		}
	}
	
	public static int[] getAttitudeInDegrees() {
		return attitudeInDegrees;
	}
}

{% endhighlight %}

<p>You can read more about android position sensors <a href="http://developer.android.com/guide/topics/sensors/sensors_position.html">here</a>. </p>

