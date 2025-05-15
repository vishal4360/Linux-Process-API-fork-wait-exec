# NAME : VISHAL C
# REG NO: 212224100062

# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:

## C Program to print process ID and parent Process ID using Linux API system calls

~~~c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    int pid = fork();

    if (pid == 0) { 
        printf("I am child, my PID is %d\n", getpid()); 
        printf("My parent PID is: %d\n", getppid()); 
        sleep(2);  // Keep child alive for verification
    } else { 
        printf("I am parent, my PID is %d\n", getpid()); 
        wait(NULL); 
    }

~~~
##OUTPUT

![image](https://github.com/user-attachments/assets/d6e253ff-9ed4-4b69-85fb-7f6fba3d6a37)

![image](https://github.com/user-attachments/assets/c699b819-fba8-4cad-8b05-d0f719fa99cf)

![image](https://github.com/user-attachments/assets/bfa38d43-fb29-48a3-a5ed-4839c517c31b)

### RESULT:
Thus the program to implement the creation of a process using fork() API is written and verified using C programming.

## C Program to create new process using Linux API system calls exec():
~~~c
#include <stdlib.h>
#include <sys/wait.h>
#include <sys/types.h>
int main()
{       int status;
        printf("Running ps with execlp\n");
        execl("ps", "ps", "ax", NULL);
        wait(&status);
        if (WIFEXITED(status))
                printf("child exited with status of %d\n", WEXITSTATUS(status));
        else
                puts("child did not exit successfully\n");
        printf("Done.\n");
printf("Running ps with execlp. Now with path specified\n");
        execl("/bin/ps", "ps", "ax", NULL);
        wait(&status);
        if (WIFEXITED(status))
                printf("child exited with status of %d\n", WEXITSTATUS(status));
        else
                puts("child did not exit successfully\n");
        printf("Done.\n");
        exit(0);}

~~~
##OUTPUT


![image](https://github.com/user-attachments/assets/dcda70cf-ef29-49c5-9a90-3746c936b86d)

![image](https://github.com/user-attachments/assets/d42260aa-8a89-45a0-9ea8-1dd076eb9b4f)

### RESULT:
Thus the program to implement the creation of a process using exec() API is written and verified using C programming.


## C Program to execute Linux system commands using Linux API system calls exit() , wait():

~~~c
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    int status;
    
    printf("Running ps with execl\n");
    if (fork() == 0) {
        execl("ps", "ps", "-f", NULL);
        perror("execl failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Running ps with execlp (without full path)\n");
    if (fork() == 0) {
        execlp("ps", "ps", "-f", NULL);
        perror("execlp failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited for execlp with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Done.\n");
    return 0;
}

~~~

## OUTPUT


![image](https://github.com/user-attachments/assets/ba3b10f6-009b-43df-85d5-2e21c83505b8)

![image](https://github.com/user-attachments/assets/97fe7275-a2ed-4089-8df4-cbca4a1d4358)

### RESULT:
Thus the program to implement the creation of a process using exit() , wait() API is written and verified using C programming.


# RESULT:
The programs are executed successfully.
