# HDH

```bash
#include <stdlib.h>
#include <stdio.h>

int main() {
        printf("print path in /home/N23DCCN106 \n");
        system("ls /home/N23DCCN106 > /home/N23DCCN106/log.txt");
        system("mkdir /home/N23DCCN106/myprogram");
        printf("Finish. \n");
        exit(0);
}

```
----
BAI 1: system()
```bash
#include <stdlib.h>
#include <stdio.h>

int main() {
    // Tạo thư mục
    system("mkdir -p /home/<MSSV>/HEDIEUHANH/THUCHANH/THUC_HANH_3");
    system("mkdir -p /home/<MSSV>/HEDIEUHANH/THUCHANH/THUC_HANH_4");

    // Tạo tập tin và ghi nội dung
    system("echo \"Great! Again!\" > /home/<MSSV>/HEDIEUHANH/THUCHANH/THUC_HANH_3/my_system.c");

    // Sao chép và hiển thị nội dung
    system("cp /home/<MSSV>/HEDIEUHANH/THUCHANH/THUC_HANH_3/my_system.c /home/<MSSV>/HEDIEUHANH/THUCHANH/THUC_HANH_4/");
    system("cat /home/<MSSV>/HEDIEUHANH/THUCHANH/THUC_HANH_4/my_system.c");

    return 0;
}

```
---
BAI 2: Thay the tien trinh
```bash
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>

int main() {
    execlp("ps", "ps", "-ax", NULL);
    perror("execlp failed");
    exit(1);
}

```
----
BAI 3: Tach tien trinh
```bash
#include <sys/types.h>
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>

int main() {
    pid_t pid;
    pid = fork();

    if (pid < 0) {
        printf("Can not create child process\n");
    } else if (pid == 0) {
        for (int i = 0; i < 2; i++) {
            printf("This is child process\n");
        }
    } else {
        for (int i = 0; i < 3; i++) {
            printf("This is parent process\n");
        }
    }

    exit(0);
}

```
----
BAI 4: Wait tien trinh con

```bash
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>

int main() {
    pid_t pid = fork();

    if (pid == 0) {
        printf("Child process running...\n");
        sleep(2);
        exit(0);
    } else {
        wait(NULL);
        printf("Parent waited for child to finish.\n");
    }

    return 0;
}

```
---BAI 5: kiem tra ma loi
```bash
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>

int main() {
    pid_t pid = fork();

    if (pid == 0) {
        printf("Child process running...\n");
        exit(5); // giả sử trả về mã lỗi 5
    } else {
        int status;
        wait(&status);

        if (WIFEXITED(status)) {
            printf("Child exited with status: %d\n", WEXITSTATUS(status));
        } else {
            printf("Child did not exit normally.\n");
        }
    }

    return 0;
}

```
