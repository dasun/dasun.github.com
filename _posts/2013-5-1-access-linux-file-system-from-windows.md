---
layout: post
title: "Access Linux File System from Windows"
thumbnail: /images/posts/access-linux-file-system-from-windows/thumbnail_200x200.png
excerpt: "Many popular Linux distributions such as Ubuntu allow accessing to Windows drives and partitions natively without having to install any utility. But this does not work in the other way around. But it is not that complicated with this utility (Ext2Read) that can be used to view and copy files and folders from LVM2 and EXT4 extents."
tags:
- linux
- windows
- ubuntu
- how-to
---
<div style="text-align:justify;">
<p class="post-image-p">
	<img class="img-polaroid" src="/images/posts/access-linux-file-system-from-windows/thumbnail_200x200.png"/>
</p>
<p>Many popular Linux distributions such as <a href="http://www.ubuntu.com/">Ubuntu</a> allow accessing to Windows drives and partitions natively without having to install any utility. But this does not work in the other way around. That means by default none of the current versions of Windows supports accessing Linux file system. Because of that to share a file from Linux to Windows we have to shut down Windows, boot into Linux and then copy the file from Linux file system to Windows file system. </p>
<p>But it is not that complicated with this utility that can be used to view and copy files and folders from LVM2 and EXT4 extents. You can download the tool Ext2Read for free from <a href="http://sourceforge.net/projects/ext2read/">here</a>. It is very easy to use and works pretty well on all the current versions of Windows including Windows 8. Please note that in Windows 7 or later versions it is required to run this tool as administrator to function properly.</p>
  Features<ul>
    <li>View and copy Ext2/Ext3/Ext4 files and folders.</li>
    <li>Ext4 Extents support.</li>
    <li>LVM2 Support</li>
    <li>Recursively copy whole directories</li>
    <li>LRU based block cache for faster concurrent access</li>
    </ul>
  <p  class="post-image-p"><img style="text-align:center;" src="/images/posts/access-linux-file-system-from-windows/ext2read.png" width="868" height="676" alt="Ext2Read"/></p>
<p>Download: <a href="http://sourceforge.net/projects/ext2read/">Ext2Read</a></p>
</div>

