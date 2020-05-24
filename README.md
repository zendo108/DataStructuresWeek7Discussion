# DataStructuresWeek7Discussion
Discussion for week 7 

Using Jeliot, execute the following algorithm which implements a buffer pool algorithm. The algorithm offers options for three different heuristics including LRU, LFU, and FIFO.

import Prog1Tools.IOTools;
import java.util.*;

class replacepage
  {
    public static void main(String args[]) {

      boolean flag;
      int f, page=0, ch, pgf=0, n, chn=0, k, pt;
      int pages[];

      //pgf-page fault

      System.out.println("Menu 1.FIFO 2. LRU 3. LFU");
      System.out.println("ENTER YOUR CHOICE: ");

      Scanner in = new Scanner(System.in);
      ch = in.nextInt();
      switch(ch)
      {
            case 1:
                pt=0;
                System.out.println("enter no. of buffers (available buffers in the pool): ");
                f=in.nextInt();
                int buffer[]=new int[f];
                for(int i=0;i<f;i++)
                {
                       buffer[i]=-1;
                 }
                 System.out.println("enter the no of pages (items to be stored): ");
                 n=in.nextInt();
                 pages=new int[n];
                 System.out.println("enter the page value (an item to place in a buffer): ");
                 for(int j=0;j<n;j++)
                        pages[j]=in.nextInt();
                 do{
                        int pg=0;
                        for(pg=0;pg<n;pg++)
                        {
                               page=pages[pg];
                                    flag=true;
                                    for(int j=0;j<f;j++)
                                    {
                                          if(page==buffer[j])
                                          {
                                              flag=false;
                                              break;
                                           }
                                      }
                                      if(flag)
                                      {
                                           buffer[pt]=page;
                                           pt++;
                                           if(pt==f) pt=0;
                                           System.out.print("buffer :");
                                           for(int j=0;j<f;j++)
                                                 System.out.print(buffer[j]+" ");
                                           System.out.println();
                                           pgf++;
                                       }
                                       else
                                      {
                                           System.out.print("buffer :");
                                           for(int j=0;j<f;j++)
                                                 System.out.print(buffer[j]+" ");
                                           System.out.println();
                                       }
                                       chn++;
                        }
                  } while(chn!=n);
                  break;

           case 2:
                k=0;
                System.out.println("enter no. of buffers (available buffers in the pool): ");
                f=in.nextInt();
                int buffer1[]=new int[f];
                int a[]=new int[f];
                int b[]=new int[f];
                for(int i=0;i<f;i++)
                {
                       buffer1[i]=-1;
                       a[i]=-1;
                       b[i]=-1;
                 }
                 System.out.println("enter the no of pages (items to be stored): ");
                 n=in.nextInt();
                 pages=new int[n];
                 System.out.println("enter the page value (an item to place in a buffer): ");
                 for(int j=0;j<n;j++)
                       pages[j]=in.nextInt();
                 do{
                       int pg=0;
                       for(pg=0;pg<n;pg++)
                       {
                           page=pages[pg];
                           flag=true;
                           for(int j=0;j<f;j++)
                           {
                                 if(page==buffer1[j])
                                 {
                                     flag=false; break;
                                  }
                            }

                               for(int j=0;j<f && flag;j++)
                            {
                                   if(buffer1[j]==a[f-1])
                                   {
                                      k=j;
                                        break;
                                    }
                             }

                            if(flag)
                            {
                                 buffer1[k]=page;
                                 System.out.println("buffer :" );
                                 for(int j=0;j<f;j++)
                                        System.out.print(buffer1[j]+" ");
                                 pgf++;
                                 System.out.println();
                             }
                             else
                             {
                                 System.out.println("buffer :" );
                                 for(int j=0;j<f;j++)
                                        System.out.print(buffer1[j]+" ");
                                 System.out.println();
                              }
                              int p=1;
                              b[0]=page;
                              for(int j=0;j<a.length;j++)
                              {
                                     if(page!=a[j] && p<f)
                                    {
                                         b[p]=a[j];
                                         p++;
                                     }
                               }
                               for(int j=0;j<f;j++)
                               {
                                     a[j]=b[j];
                                }
                                     chn++;
                                }
                           } while(chn!=n);
                           break;

                    case 3:
                          k=0;
                          pgf=0;
                          int sml;
                          System.out.println("enter no. of buffers (available buffers in the pool): ");
                               f=in.nextInt();
                          int buffer2[]=new int[f];
                          int cnt[]=new int [f];
                          flag=true;

                          for(int i=0;i<f;i++)
                          {
                                buffer2[i]=-1;
                                cnt[i]=0;
                           }
                          System.out.println("enter the page value (an item to place in a buffer): ");
                          n=in.nextInt();
                          pages=new int[n];
                          System.out.println("enter the page value (an item to place in a buffer): ");
                          for(int j=0;j<n;j++)
                                 pages[j]=in.nextInt();
                          do
                          {
                                 int pg=0;
                                 for(pg=0;pg<n;pg++)
                                 {
                                        page=pages[pg];
                                        flag=true;
                                        for(int j=0;j<f;j++)
                                        {
                                               if(page==buffer2[j])
                                               {
                                                      flag=false;
                                                      cnt[j]++;
                                                      break;
                                                }
                                         }
                                         if(flag)
                                        {
                                              sml=cnt[0];
                                              for(int j=0;j<f;j++)
                                              {
                                                     if(cnt[j]<sml)
                                                     {
                                                           sml=cnt[j];
                                                           break;
                                                      }

                                         }
                                         for(int j=0;j<f;j++)
                                        {
                                                if(sml==cnt[j] )
                                                   {
                                                      buffer2[j]=page;
                                                       k=j;
                                                       break;
                                                 }
                                         }
                                         cnt[k]=1;
                                         System.out.print("buffer :");
                                         for(int j=0;j<f;j++)
                                         {
                                               System.out.print(buffer2[j]+" ");
                                               System.out.println();
                                               pgf++;
                                          }
                                    }
                                    else
                                    {
                                         System.out.print("buffer :");
                                         for(int j=0;j<f;j++)
                                               System.out.print(buffer2[j]+" ");
                                         System.out.println();
                                     }
                                    chn++;
                                }
                          } while(chn!=n);
                            break;
                    }
             }
     }

The algorithm will request the following information to be entered.

Menu: 1. FIFO, 2. LRU, 3. LFU

It would be recommended that you increase the execution speed of Jeliot to its maximum or run this java routine directly from the java interpreter due to the complexity of the code. You can slow down the execution, if required, to understand elements of the execution.

For this assignment you must run the algorithm for each menu option as specified and respond to the questions.

For option 1 on the menu (FIFO), run the algorithm and observe how the algorithm responds. For this iteration use the following input:

Buffers: 2      (the size of the buffer pool)

Pages: 6        (the number of items to place into the pool. Note that there are more pages than
                         frames which means that the algorithm will force some pages out of the buffer
                         pool)

Page Values:      5, 5, 5, 10, 20, 5

Questions:

1. Describe the heuristic used in menu option 1.

2. Under what condition will this heuristic not be efficient? In this context an efficient buffer, is one that has the highest potential to provide a block of data out of the buffer and not have to go back to disk. In your answer consider whether this heuristic is the most effective approach is the value 5 is used more frequently than any other value.

3. Describe a situation where this heuristic would be efficient. For a hint think about read-ahead capabilities.

For option 2 on the menu (LRU), run the algorithm and observe how the algorithm responds. For this iteration use the following input:

Buffers: 2

Pages: 6

Page Values: 5, 10, 5, 10, 20, 5

Questions:

1. Describe the heuristic used in menu option 2.

2. Provide an example or define the characteristics of a situation where this heuristic would be efficient. In this context, efficient, means a situation where required the data can be supplied from the buffer and not from an external source such as the disk. A hint is to look at what data occurs most frequently. In this case it is the value 5.

For option 3 on the menu (LFU), run the algorithm twice and observe how the algorithm responds. For the first iteration of this option use the following input:

Buffers: 2

Pages: 6

Page Values: 5, 10, 5, 10, 20, 5

For the second iteration of this option use the following input:

Buffers: 2

Pages: 6

Page Values: 5, 10, 20, 25, 30, 35

Questions:

1. Describe the heuristic used in menu option 3.

2. What happens when no integer is repeated in the input page values?

3. Describe what happens in the buffer pool when a value is repeated in the page values.

Complete the preceding exercise and develop a response to each of the questions. Post your responses to the discussion forum. If you have arrived at a different answer or analysis than your peers, discuss your findings with your peers and attempt to determine whose analysis is most accurate.

You must post your initial response before being able to review other student’s responses. Once you have made your first response, you will be able to reply to other student’s posts. You are expected to make a minimum of 3 responses to your fellow student’s posts.
