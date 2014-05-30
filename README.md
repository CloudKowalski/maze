import java.util.*;
import java.io.*;
import java.lang.*;
import static java.lang.System.*;

public class Maze
{
 
 public void run()throws Exception
 {
  Scanner in=new Scanner(new File("maze.dat"));
  int run=in.nextInt();
  in.nextLine();
  char[][]mze;
  boolean[][]visited;
  for(int runcount=0;runcount<run;runcount++)
  {
   int copy=runcount+1;
   visited=new boolean[20][20];
   mze=new char[20][20];
   for(int r=0;r<20;r++)
    mze[r]=in.nextLine().toCharArray();
   int r=-1;
   int c=-1;
   if(runcount!=run-1)
   in.nextLine();

   
 main:for(int row=0;row<20;row++)
    for(int col=0;col<19;col++)
    {
     if(mze[row][col]=='S')
     {
      r=row;
      c=col;
      break main;
     }
    }

   if(recur(mze,r,c,visited))
   {
    System.out.println("Maze # "+copy+": YES");
   }
   else
    System.out.println("Maze # "+copy+": NO");
  }
 }
 
 public boolean recur(char[][]mze,int r,int c,boolean[][]visited)
 {
  
  int endx=0;
  int endy=0;
 mainloop: for(int x=0;x<20;x++)
    {
     for(int y=0;y<19;y++)
     {
      if(mze[x][y]=='E')
      {
       endx=x;
       endy=y;
       break mainloop;
      }
     }
    }
   
   if( endx>0 && mze[endx-1][endy]=='#' )
   {
    if(endx<=19 || mze[endx+1][endy]=='#')
        if( endy>0 && mze[endx][endy-1]=='#' )
        {
         if(endy<=19 || mze[endx][endy+1]=='#')
          return false;
        }
   }
  
  if(!visited[r][c] &&r<20 && r>=0 && c<19 && c>=0)
  {

   if(mze[r][c]=='.')
   {
    mze[r][c]='S';
   }
   else if(mze[r][c]=='#')
    return false;
   
  else if(mze[r][c]=='E')
    return true;
    
   visited[r][c]=true;
   if(!visited[r+1][c] && recur(mze,r+1,c,visited))
   {
    
    return true;
   }
   if(!visited[r-1][c] &&  recur(mze,r-1,c,visited)) return true;
   if(!visited[r][c+1] &&  recur(mze,r,c+1,visited))  return true;
   if(!visited[r][c-1] &&  recur(mze,r,c-1,visited)) return true;
    

  }
  return false;
 }
 
 public static void main(String[]Kowalski)throws Exception
 {
  Maze a=new Maze();
  a.run();
 }
}
