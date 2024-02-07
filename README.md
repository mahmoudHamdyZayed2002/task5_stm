# task5_stm
## my shell to be used in linux

code:
***

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

char **parsing_string(char * user_string , int* arg_number){
	int str_len = strlen(user_string);
	char **array_parsed=NULL;
	int arr_index =0;
	*arg_number=1;
	while (arr_index < str_len) {
	if (user_string[arr_index] == ' ') {
	    (*arg_number)++;
	}
	arr_index++;
    }
	char *token = strtok(user_string," ");
	array_parsed = (char**)malloc(((*arg_number)+1) * sizeof(char*));
	int index =0;
for (arr_index = 0; arr_index < *arg_number; arr_index++) {
	int token_size = strlen(token);
	array_parsed[arr_index] = (char *) malloc(token_size * sizeof(char));
	strcpy(array_parsed[arr_index], token);
	token = strtok(NULL, " ");	//make token points to the next word
    }

    
	return array_parsed;
	
}


char *str_in;
size_t n;

int main (void)
{
  printf ("my pid =%d , my parent pid =%d \n", getpid (), getppid ());
  getchar ();

  while (1)
    {
    
      char **arguments=NULL;
      int arg_num=0;
      char path [30]={0};
      char * path2=getcwd(path,30);
      printf (" %s >>>>>>>> ",path);
      getline (&str_in, &n, stdin);
      int len = strlen (str_in);
      str_in[len - 1] = 0;
      if (strlen (str_in) == 0)
	{
	  continue;
	}
      else
	{
	}
        arguments = parsing_string(str_in,&arg_num);
	for(int i =0 ; i<arg_num;i++){
                printf("1111111111111111aguments[%d] = %s /n ",i,arguments[i]);

        }
	printf("number of parsing strings = %d\n",arg_num);
	
       if ((!(strcmp ("exit", arguments[0]))))
	{
	  printf ("you are wilcome\n");

	  break;
	}
        else if(!(strcmp(arguments[0] ,"cd"))){
		      chdir (arguments[1]);
      
      }
      else
	{
      pid_t ret_pid = fork ();
      if (ret_pid < 0)
	{
	  printf ("error generation \n");
	}
      else if (ret_pid > 0)
	{

	  int status;
	  wait (&status);
	  printf ("the last command status =%d , exit status =%d\n", status,
		  WIFEXITED (status));
	}
      else if (ret_pid == 0)
	{
	
	for(int i =0 ; i<arg_num;i++){
		printf("22222222arguments[%d] = %s \n ",i,arguments[i]);

	}	
	  execvp (arguments[0], arguments);
	  printf ("nter correct command\n");
	  return 99;
	}
	}
    }

  return 0;
}
***
out puts :
*** 
/home/mahmoud/task4/task4 >>>>>>>> 
 /home/mahmoud/task4/task4 >>>>>>>> 
 /home/mahmoud/task4/task4 >>>>>>>> 
 /home/mahmoud/task4/task4 >>>>>>>> 
 /home/mahmoud/task4/task4 >>>>>>>> 
 /home/mahmoud/task4/task4 >>>>>>>> 
 /home/mahmoud/task4/task4 >>>>>>>> 
 /home/mahmoud/task4/task4 >>>>>>>> 
 /home/mahmoud/task4/task4 >>>>>>>> ls
number of parsing strings = 1
1  dd  dup.c  dup.exe  ffffff  file  task41.c  task4_dynamic.c	task4_dynamic.exe  task4.exe  test1.c  test1.exe  test222.exe  test2.c	test2.exe  testced.c  testced.exe
the last command status =0 , exit status =1
 /home/mahmoud/task4/task4 >>>>>>>> pwd
number of parsing strings = 1
/home/mahmoud/task4/task4
the last command status =0 , exit status =1
 /home/mahmoud/task4/task4 >>>>>>>> cd /home/mahmoud
number of parsing strings = 2
 /home/mahmoud >>>>>>>> ls
number of parsing strings = 1
1    1.exe  1.o  3.c	a.out  dir1  fil41   fil445  file42  file51  filrr  ll	     mycp.c    myecho.c    myhello  repos  task2      task2.out  task4		  text
1.c  1.i    1.s  3.exe	dd     dir2  fil444  file41  file44  filr2   kkkk   mmmmmmm  mycp.exe  myecho.exe  ooooo    snap   task2.0ut  task3	 task4_dynamic.c
the last command status =0 , exit status =1
 /home/mahmoud >>>>>>>> mkdir task5_5   
number of parsing strings = 2
the last command status =0 , exit status =1
 /home/mahmoud >>>>>>>> ls
number of parsing strings = 1
1    1.exe  1.o  3.c	a.out  dir1  fil41   fil445  file42  file51  filrr  ll	     mycp.c    myecho.c    myhello  repos  task2      task2.out  task4		  task5_5
1.c  1.i    1.s  3.exe	dd     dir2  fil444  file41  file44  filr2   kkkk   mmmmmmm  mycp.exe  myecho.exe  ooooo    snap   task2.0ut  task3	 task4_dynamic.c  text
the last command status =0 , exit status =1
 /home/mahmoud >>>>>>>> cd /home/mahmoud/task5_5
number of parsing strings = 2
 /home/mahmoud/task5_5 >>>>>>>> touch denoooo
number of parsing strings = 2
the last command status =0 , exit status =1
 /home/mahmoud/task5_5 >>>>>>>> ls
number of parsing strings = 1
denoooo
the last command status =0 , exit status =1
 /home/mahmoud/task5_5 >>>>>>>> vim maaa
number of parsing strings = 2
the last command status =0 , exit status =1
 /home/mahmoud/task5_5 >>>>>>>> ls
number of parsing strings = 1
denoooo
the last command status =0 , exit status =1
 /home/mahmoud/task5_5 >>>>>>>> pwd
number of parsing strings = 1
/home/mahmoud/task5_5
the last command status =0 , exit status =1
 /home/mahmoud/task5_5 >>>>>>>> nano mmmm
number of parsing strings = 2
the last command status =0 , exit status =1
 /home/mahmoud/task5_5 >>>>>>>> ls
number of parsing strings = 1
denoooo  mmmm
the last command status =0 , exit status =1
 /home/mahmoud/task5_5 >>>>>>>> vim mahm
number of parsing strings = 2
the last command status =0 , exit status =1
 /home/mahmoud/task5_5 >>>>>>>> ls
number of parsing strings = 1
denoooo  mahm  mmmm
the last command status =0 , exit status =1
 /home/mahmoud/task5_5 >>>>>>>> ls
number of parsing strings = 1
denoooo  mahm  mmmm
the last command status =0 , exit status =1
 /home/mahmoud/task5_5 >>>>>>>> pwd
number of parsing strings = 1
/home/mahmoud/task5_5
the last command status =0 , exit status =1
 /home/mahmoud/task4/task4 >>>>>>>> echo llfl fkfkfk fmfmfm fmfmfm fmfmfmf fmfmfm fmfmmf fmfmfmfmf kffkfkf
number of parsing strings = 10
llfl fkfkfk fmfmfm fmfmfm fmfmfmf fmfmfm fmfmmf fmfmfmfmf kffkfkf
the last command status =0 , exit status =1
 /home/mahmoud/task4/task4 >>>>>>>> exit
number of parsing strings = 1
you are wilcome
***
### i will improve my own shell and try to add other fetures 
