#include <unistd.h>
#include <sys/wait.h>
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <iostream>


int main(int argc, char *argv[])
  {
  
    using std::cout;
	using std::endl;
	using std::cerr;
  
   int     pipefd[2];
   pid_t   Gpid;
   pipe(pipefd);
   pid_t Cpid;
   int status, status1;
   //int in, out;
   
   Gpid = fork();
  // pid = childpid;
   
   char *newargv[] = { NULL };
   char *newenviron[] = { NULL };
   
   //in = open("in", O_RDONLY);
  
   		if(Gpid == 0) // its a child process
	   { 
	   
			//if the process is the child then connect its output to the write end of the pipe you created
			//close the read end of the pipe (not needed if using O_CLOEXEC with pipe2)
			//exec generator
		
			//close(pipefd[0]);          /* Close unused read end */
            //write(pipefd[1], argv[1], char(strlen(argv[1])));
            //close(pipefd[1]);          /* Reader will see EOF */
            //wait(NULL); 
            //popen("./generator","r");  
            
            dup2(pipefd[1], 1);

      		// close unused hald of pipe

      		close(pipefd[1]);
            
			execve("./generator", newargv, newenviron); // ./dispatcher.cpp ./generator ./consumer
			//pclose(file);
			//write(fd[1], string, (strlen(string)+1);
			
			exit(0);
			
	   }
	   
	   //pid_c = getpid();
	   
	   Cpid = fork();
	   
	   if (Cpid == 0)
	   {
	   		//if the process is the child then connect its input to the read end of the pipe you created
			//close the write end of the pipe (not needed if useing O_CLOEXEC either with pipe2, or a call to fcntl(3))
			//exec consumer
			
			// replace standard output with output part of pipe

      		dup2(pipefd[0], 0);

      		// close unused hald of pipe

     		close(pipefd[1]);

			execve("./consumer", newargv, newenviron); // ./dispatcher.cpp ./generator ./consumer
			
			exit(0);
	   }
	   
	   //Cpid = waitpid(Cpid, &status, WNOHANG);  //WUNTRACED  //  WNOHANG 
	   
	   sleep(1);
	   
	   kill(Gpid, SIGTERM);
	   //kill(Cpid, SIGINT);
	   
	   waitpid(Gpid, &status, 0);  //WUNTRACED  //  WNOHANG
	   
	   cerr << "Child[" << Gpid << "]: exited with status 0" << endl; 
	   
	   //waitpid(Cpid, &status, 0);
	   
	   //wait(&status); // waiting for consumer child to end
	   
	   //Cpid = waitpid(Cpid, &status, 0);
	   
	   cerr << "Child[" << Cpid << "]: exited with status 0" << endl;
	   
	   //pid = waitpid(pid, &status, options);
	   //kill(childpid, SIGINT);
   
   return 0;
   
  }
