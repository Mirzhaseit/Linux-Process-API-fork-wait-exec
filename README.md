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

## 1. C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls

```bash
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
}
```



## OUTPUT
<img width="877" height="334" alt="image" src="https://github.com/user-attachments/assets/3d4facfd-717c-414b-b85d-8fb2501389fa" />



## 2. C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family

```bash
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
  ```


## OUTPUT
<img width="745" height="599" alt="image" src="https://github.com/user-attachments/assets/f546893d-3f40-4567-8556-5b7e2aa216ba" />
<img width="668" height="589" alt="image" src="https://github.com/user-attachments/assets/88904f1b-916b-4517-81fe-193bcaa787a0" />
<img width="723" height="590" alt="image" src="https://github.com/user-attachments/assets/d2d0adba-4547-4ed5-85cb-de3e3840ba1c" />
<img width="710" height="593" alt="image" src="https://github.com/user-attachments/assets/0c858c73-44aa-44c7-8d60-253073490ad8" />
<img width="786" height="589" alt="image" src="https://github.com/user-attachments/assets/429b2ef3-d0e6-4f5d-b92c-48629ed1963d" />
<img width="792" height="585" alt="image" src="https://github.com/user-attachments/assets/02ccf562-a440-491c-b10f-e6bd584e5416" />
<img width="771" height="600" alt="image" src="https://github.com/user-attachments/assets/36f8ec55-52ac-4525-8064-28733a5e5e84" />
<img width="749" height="603" alt="image" src="https://github.com/user-attachments/assets/d72fe6e7-4db3-4eb1-a520-755f2e612680" />
<img width="728" height="199" alt="image" src="https://github.com/user-attachments/assets/44100d2b-b736-465c-b32f-3ccff2867c8d" />



## 3. C Program to execute Linux system commands using Linux API system calls exec() family

```bash
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
```
## OUTPUT
<img width="880" height="386" alt="image" src="https://github.com/user-attachments/assets/c02ff78a-5bff-4568-a53f-4efe5c16c2a4" />





# RESULT:
The programs are executed successfully.
