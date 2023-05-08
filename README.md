Download Link: https://assignmentchef.com/product/solved-ucs1411-exercise-5-interprocess-communications-on-shared-memory
<br>
InterProcess Communications using Shared Memory

<u>Study the following system calls.</u>

Shared memory – shmget, shmat, shmdt, shmctl

<u>Additional system calls (For your understanding)</u>

Pipe – pipe, mkfifo, mknod, open, read, write, close

Message Queue – msgget, msgsnd, msgrcv, msgctl

<u>Aim:</u>

Develop the following applications that uses interprocess communication concepts using shared memory.

1.Develop an application for getting a name in parent and convert it into uppercase in child using shared memory.

2.Develop an client / server application for file transfer using shared memory.

<ol start="3">

 <li>Develop an client/server chat application using shared memory.</li>

</ol>

<u>Comment:</u>

This program should be run as a single program in which parent is one process and child is another process.

<u>Client / server:</u>

Keep common code and parent code in one program as server.c

Keep common code and child code in another program as client.c

Run server.c in one terminal and client.c in another terminal. Communicate between the two processes.




Example :

Shared memory :

#include &lt;sys/ipc.h&gt;

# define NULL 0

#include &lt;sys/shm.h&gt;

#include &lt;sys/types.h&gt;

# include&lt;unistd.h&gt;

# include&lt;stdio.h&gt;

# include&lt;stdlib.h&gt;

# include&lt;string.h&gt;

#include &lt;sys/wait.h&gt;

#include &lt;stdio_ext.h&gt;

// parent writing a char in shared memory and child reads it and prints it. int main()

{ int pid; char *a,*b,c; int id,n,i;

// you can create a shared memory between parent and child here or you can //create inside them separately.

id=shmget(111,50,IPC_CREAT | 00666);

pid=fork(); if(pid&gt;0) //parent

{

// id=shmget(111,50,IPC_CREAT | 00666); a=shmat(id,NULL,0);

a[0]=’d’;

wait(NULL); shmdt(a);

} else //child

{ sleep(3);

//id=shmget(111,50,0); b=shmat(id,NULL,0); printf(“
 child %c
”,b[0]);

shmdt(b); }         shmctl(id, IPC_RMID,NULL);

}