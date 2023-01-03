![image-20221228213201935](C:\Users\rahul\AppData\Roaming\Typora\typora-user-images\image-20221228213201935.png)

![image-20221228220526448](C:\Users\rahul\AppData\Roaming\Typora\typora-user-images\image-20221228220526448.png)

![image-20221228220542620](C:\Users\rahul\AppData\Roaming\Typora\typora-user-images\image-20221228220542620.png)

![image-20221228220604038](C:\Users\rahul\AppData\Roaming\Typora\typora-user-images\image-20221228220604038.png)





# **A File System**



![image-20221228220635456](C:\Users\rahul\AppData\Roaming\Typora\typora-user-images\image-20221228220635456.png)

### **In GIT the content of the files are stored in the ogjects called BLOB**

BLOB = Binary Large Object

How it is differenet for the files linux file ?
File also contains the metadata say for example dat of creatin, owners etc etc.. However the BLOBs on the other hands are just the contents, blob doesn't remeber its creation date, name  any thing but ONLY the contents.

Every BLOB in GIT, is identified by SHA1 hash



In git the quivelant of the Directory is TREE, tREE is basically directory listing, refering to BLOB as well as other tree. TREEs are alos identified as there SHA1 hases as well.



![image-20221228221256646](C:\Users\rahul\AppData\Roaming\Typora\typora-user-images\image-20221228221256646.png)



how this structure looks like ???



Isn't it a file system ?



Now let's take the snapshot of the file system, so that we can store all the files along with there contents.

In Git COMMIT is basically taking the snapshot

A COMMIT object includes a pointer to the  main tree, which is th root directory, along with this commit also stores 

metadata, such as commiter , commit time  and commit messages. Most of the time COMMIT would also have one more parent commit.

same as abve the COMMIT objects are also identified as there SHA1 HASHES.





![image-20221228221824608](C:\Users\rahul\AppData\Roaming\Typora\typora-user-images\image-20221228221824608.png)



eVERY COMMIT  sees the entire SNAPSHOTS not just the DELTA from the previous commits ???

What does this mean ?

It looks to me that we have to store lot of duplicate data , on every commit

Lets see how exactly it works?

Say for example you have chnaged the content of the file.



![image-20221228222116584](C:\Users\rahul\AppData\Roaming\Typora\typora-user-images\image-20221228222116584.png)



This chnage means that,, you have new BLOB with new SHA1 hash





![image-20221228222219185](C:\Users\rahul\AppData\Roaming\Typora\typora-user-images\image-20221228222219185.png)



![image-20221228222252381](C:\Users\rahul\AppData\Roaming\Typora\typora-user-images\image-20221228222252381.png)



![image-20221228222336152](C:\Users\rahul\AppData\Roaming\Typora\typora-user-images\image-20221228222336152.png)



As  long as the object  doesn't chnage we don't chnage it again.



![image-20221228222425056](C:\Users\rahul\AppData\Roaming\Typora\typora-user-images\image-20221228222425056.png)