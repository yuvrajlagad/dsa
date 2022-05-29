#include <iostream>
#include<fstream>
#include<cstring>
#include<iomanip>
using namespace std;
const int MAX=20;
class Employee
{
 int empid;
 char name[20],city[20];
 char role;
 int salary;
public:
 Employee()
{
  strcpy(name,"");
  strcpy(city,"");
  empid=salary=role=0;
}
 Employee(int empid,char name[MAX],int salary,char role,char city[MAX])
 {
  strcpy(this->name,name);
  strcpy(this->city,city);
  this->empid=empid;
  this->salary=salary;
  this->role=role;
 }
 int getRollNo()
 {
  return empid;
 }
 void displayRecord()
 {

  cout<<endl<<setw(5)<<empid<<setw(20)<<name<<setw(5)<<salary<<setw(5)<<role<<setw(10)<<city;
 }
};
//==========File Operations ===========
class FileOperations
{
 fstream file;
public:
 FileOperations(char* filename)
{
file.open(filename,ios::in|ios::out|ios::ate|ios::binary);
}
 void insertRecord(int empid, char name[MAX],int salary, char role,char city[MAX])
 {
  Employee e1(empid,name,salary,role,city);
  file.seekp(0,ios::end);
  file.write((char *)&e1,sizeof(Employee));
  file.clear();
 }
 void displayAll()
 {
  Employee e1;
  file.seekg(0,ios::beg);
  while(file.read((char *)&e1, sizeof(Employee)))
  {
   e1.displayRecord();
  }
  file.clear();
 }
 void displayRecord(int empid)
 {
  Employee e1;
  file.seekg(0,ios::beg);
  bool flag=false;
  while(file.read((char*)&e1,sizeof(Employee)))
  {
   if(e1.getRollNo()==empid)
   {
    e1.displayRecord();
    flag=true;
    break;
   }
  }
  if(flag==false)
  {
   cout<<"\nRecord of "<<empid<<"is not present.";
  }
  file.clear();
 }
 void deleteRecord(int empid)
 {
  ofstream outFile("new.dat",ios::binary);
  file.seekg(0,ios::beg);
  bool flag=false;
  Employee e1;

  while(file.read((char *)&e1, sizeof(Employee)))
  {
   if(e1.getRollNo()==empid)
   {
    flag=true;
    continue;
   }
   outFile.write((char *)&e1, sizeof(Employee));
  }
  if(!flag)
  {
   cout<<"\nRecord of "<<empid<<" is not present.";
  }
  file.close();
  outFile.close();
  remove("Employee.dat");
  rename("new.dat","Employee.dat");
  file.open("Employee.dat",ios::in|ios::out|ios::ate|ios::binary);
 }
 ~FileOperations()
 {
  file.close();
  cout<<"\nFile Closed.";
 }
};
int main() {
 ofstream newFile("Employee.dat",ios::app|ios::binary);
  newFile.close();
  FileOperations file((char*)"Employee.dat");
     int empid,salary,choice=0;
     char role;
     char name[MAX],address[MAX];
     while(choice!=5)
     {
         //clrscr();
         cout<<"\n*****Employee Database*****\n";
         cout<<"1) Add New Record\n";
         cout<<"2) Display All Records\n";
         cout<<"3) Display by Employee ID\n";
         cout<<"4) Deleting a Record\n";
         cout<<"5) Exit\n";
         cout<<"Choose your choice : ";
         cin>>choice;
         switch(choice)
         {
             case 1 : //New Record
               cout<<endl<<"Enter Employee ID and name : \n";
               cin>>empid>>name;
               cout<<"Enter Year and Designation : \n";
               cin>>salary>>role;
               cout<<"Enter address : \n";
               cin>>address;
               file.insertRecord(empid,name,salary,role,address);
               cout<<"\nRecord Inserted.";
               break;
             case 2 :
              cout<<endl<<setw(5)<<"ID"<<setw(20)<<"NAME"<<setw(5)<<"SALARY"<<setw(5)<<"ROLE"<<setw(10)<<"CITY";
               file.displayAll();
               break;
             case 3 :
               cout<<"Enter Employee ID";
               cin>>empid;
                file.displayRecord(empid);

               break;
             case 4:
               cout<<"Enter Employee ID";
               cin>>empid;
               file.deleteRecord(empid);
               break;
            case 5 :break;
         }

     }

 return 0;
}
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  #include<iostream>
#include<fstream>
#include<cstring>
using namespace std;
class tel
 {

 public:
 int rollNo,roll1;
 char name[10];
 char div;
 char address[20];
 void accept()
 {
  cout<<"\n\tEnter Roll Number : ";
  cin>>rollNo;
  cout<<"\n\tEnter the Name : ";
  cin>>name;
  cout<<"\n\tEnter the Division:";
  cin>>div;
  cout<<"\n\tEnter the Address:";
  cin>>address;
 }
        void accept2()
        {
               cout<<"\n\tEnter the Roll No. to modify : ";
               cin>>rollNo;
        }
        void accept3()
        {
              cout<<"\n\tEnter the name to modify : ";
              cin>>name;
        }
        int getRollNo()
        {
         return rollNo;
        }
 void show()
 {

  cout<<"\n\t"<<rollNo<<"\t\t"<<name<<"\t\t"<<div<<"\t\t"<<address;
 }
};
int main()
{
 int i,n,ch,ch1,rec,start,count,add,n1,add2,start2,n2,y,a,b,on,oname,add3,start3,n3,y1,add4,start4,n4;
 char name[20],name2[20];
 tel t1;
 count=0;
 fstream g,f;
 do
 {
  cout<<"\n>>>>>>>>>>>>>>>>>>>>>>MENU<<<<<<<<<<<<<<<<<<<<";
  cout<<"\n1.Insert and overwrite\n2.Show\n3.Search & Edit(number)\n4.Search & Edit(name)\n5.Search & Edit(onlynumber)\n6.Search & edit(only name)\n 7.Delete a Student Record\n 8.Exit\n\tEnter the Choice\t:";
  cin>>ch;
  switch(ch)
  {
  case 1:
   f.open("StuRecord.txt",ios::out);
   x:t1.accept();
   f.write((char*) &t1,(sizeof(t1)));
   cout<<"\nDo you want to enter more records?\n1.Yes\n2.No";
   cin>>ch1;
    if(ch1==1)
     goto x;
    else
    {
     f.close();
     break;
    }

  case 2:
   f.open("StuRecord.txt",ios::in);
   f.read((char*) &t1,(sizeof(t1)));
   //cout<<"\n\tRoll No.\t\tName \t\t Division \t\t Address";
   while(f)
   {
    t1.show();
    f.read((char*) &t1,(sizeof(t1)));
   }
   f.close();
   break;
  case 3:
   cout<<"\nEnter the roll number you want to find";
   cin>>rec;
   f.open("StuRecord.txt",ios::in|ios::out);
   f.read((char*)&t1,(sizeof(t1)));
   while(f)
   {
    if(rec==t1.rollNo)
    {
     cout<<"\nRecord found";
     add=f.tellg();
     f.seekg(0,ios::beg);
           start=f.tellg();
     n1=(add-start)/(sizeof(t1));
     f.seekp((n1-1)*sizeof(t1),ios::beg);
     t1.accept();
     f.write((char*) &t1,(sizeof(t1)));
     f.close();
     count++;
     break;
    }
    f.read((char*)&t1,(sizeof(t1)));
       }
   if(count==0)
          cout<<"\nRecord not found";
   f.close();
   break;

  case 4:
   cout<<"\nEnter the name you want to find and edit";
   cin>>name;
   f.open("StuRecord.txt",ios::in|ios::out);
   f.read((char*)&t1,(sizeof(t1)));
   while(f)
   {
   y=(strcmp(name,t1.name));
   if(y==0)
   {
    cout<<"\nName found";
    add2=f.tellg();
    f.seekg(0,ios::beg);
    start2=f.tellg();
    n2=(add2-start2)/(sizeof(t1));
    f.seekp((n2-1)*sizeof(t1),ios::beg);
    t1.accept();
    f.write((char*) &t1,(sizeof(t1)));
    f.close();
    break;
   }
          f.read((char*)&t1,(sizeof(t1)));
   }
   break;
      case 5:
            cout<<"\n\tEnter the roll number you want to modify";
            cin>>on;
            f.open("StuRecord.txt",ios::in|ios::out);
            f.read((char*) &t1,(sizeof(t1)));
            while(f)
            {
              if(on==t1.rollNo)
              {
                cout<<"\n\tNumber found";
                add3=f.tellg();
                f.seekg(0,ios::beg);
                start3=f.tellg();
                n3=(add3-start3)/(sizeof(t1));
                f.seekp((n3-1)*(sizeof(t1)),ios::beg);
                t1.accept2();
                f.write((char*)&t1,(sizeof(t1)));
                f.close();
                break;
              }
              f.read((char*)&t1,(sizeof(t1)));
           }
           break;
      case 6:
            cout<<"\nEnter the name you want to find and edit";
   cin>>name2;
   f.open("StuRecord.txt",ios::in|ios::out);
   f.read((char*)&t1,(sizeof(t1)));
   while(f)
   {
   y1=(strcmp(name2,t1.name));
   if(y1==0)
   {
    cout<<"\nName found";
    add4=f.tellg();
    f.seekg(0,ios::beg);
    start4=f.tellg();
    n4=(add4-start4)/(sizeof(t1));
    f.seekp((n4-1)*sizeof(t1),ios::beg);
    t1.accept3();
    f.write((char*) &t1,(sizeof(t1)));
    f.close();
    break;
   }
          f.read((char*)&t1,(sizeof(t1)));
   }
   break;
    case 7:
      int roll;
      cout<<"Please Enter the Roll No. of Student Whose Info You Want to Delete: ";
     cin>>roll;
     f.open("StuRecord.txt",ios::in);
     g.open("temp.txt",ios::out);
     f.read((char *)&t1,sizeof(t1));
     while(!f.eof())
     {
        if (t1.getRollNo() != roll)
          g.write((char *)&t1,sizeof(t1));
         f.read((char *)&t1,sizeof(t1));
     }
    cout << "The record with the roll no. " << roll << " has been deleted " << endl;
     f.close();
     g.close();
     remove("StuRecord.txt");
     rename("temp.txt","StuRecord.txt");
      break;
    case 8:
       cout<<"\n\tThank you";
       break;


        }
  }while(ch!=8);
}

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  #include <iostream>
using namespace std;

void
MaxHeapify (int a[], int i, int n)
{
  int j, temp;
  temp = a[i];
  j = 2 * i;

  while (j <= n)
    {
      if (j < n && a[j + 1] > a[j])
	j = j + 1;

      if (temp > a[j])
	break;

      else if (temp <= a[j])
	{
	  a[j / 2] = a[j];
	  j = 2 * j;
	}
    }
  a[j / 2] = temp;
  return;
}

void
MinHeapify (int a[], int i, int n)
{
  int j, temp;
  temp = a[i];
  j = 2 * i;

  while (j <= n)
    {
      if (j < n && a[j + 1] < a[j])
	j = j + 1;

      if (temp < a[j])
	break;

      else if (temp >= a[j])
	{
	  a[j / 2] = a[j];
	  j = 2 * j;
	}
    }
  a[j / 2] = temp;
  return;
}

void
MaxHeapSort (int a[], int n)
{
  int i, temp;
  for (i = n; i >= 2; i--)
    {

      temp = a[i];
      a[i] = a[1];
      a[1] = temp;

      MaxHeapify (a, 1, i - 1);
    }
}

void
MinHeapSort (int a[], int n)
{
  int i, temp;
  for (i = n; i >= 2; i--)
    {

      temp = a[i];
      a[i] = a[1];
      a[1] = temp;

      MinHeapify (a, 1, i - 1);
    }
}

void
Build_MaxHeap (int a[], int n)
{
  int i;
  for (i = n / 2; i >= 1; i--)
    MaxHeapify (a, i, n);
}

void
Build_MinHeap (int a[], int n)
{
  int i;
  for (i = n / 2; i >= 1; i--)
    MinHeapify (a, i, n);
}

int
main ()
{
  int n, i;
  cout << "\nEnter the number of Students : ";
  cin >> n;
  n++;
  int arr[n];
  for (i = 1; i < n; i++)
    {
      cout << "Enter the marks :  " << i << ": ";
      cin >> arr[i];
    }

  Build_MaxHeap (arr, n - 1);
  MaxHeapSort (arr, n - 1);


  int max, min;
  cout << "\nSorted Data : ASCENDING : ";

  for (i = 1; i < n; i++)
    cout << "->" << arr[i];
  min = arr[1];
  Build_MinHeap (arr, n - 1);
  MinHeapSort (arr, n - 1);
  cout << "\nSorted Data : DESCENDING: ";
  max = arr[1];
  for (i = 1; i < n; i++)
    cout << "->" << arr[i];
  cout << "\nMaximum Marks : " << max << "\nMinimum marks : " << min;
  return 0;
}

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  #include <iostream>
#include<string>
using namespace std;
class dictionary;
class node
{
  string word, meaning;
  node *left, *right;
public:
    friend class dictionary;
    node ()
  {
    left = NULL;
    right = NULL;

  }
  node (string word, string meaning)
  {
    this->word = word;
    this->meaning = meaning;
    left = NULL;
    right = NULL;
  }
};

class dictionary
{
  node *root;
public:
    dictionary ()
  {
    root = NULL;
  }
  void create ();
  void inorder_rec (node * rnode);
  void postorder_rec (node * rnode);
  void inorder ()
  {
    inorder_rec (root);
  }
  void postorder ();

  bool insert (string word, string meaning);
  int search (string key);

};

int
dictionary::search (string key)
{
  node *tmp = root;
  int count;
  if (tmp == NULL)
    {
      return -1;
    }
  if (root->word == key)
    return 1;
  while (tmp != NULL)
    {

      if ((tmp->word) > key)
	{
	  tmp = tmp->left;
	  count++;
	}
      else if ((tmp->word) < key)
	{
	  tmp = tmp->right;
	  count++;
	}
      else if (tmp->word == key)
	{
	  return ++count;
	}
    }
  return -1;

}

void
dictionary::postorder ()
{
  postorder_rec (root);
}

void
dictionary::postorder_rec (node * rnode)
{
  if (rnode)
    {
      postorder_rec (rnode->right);
      cout << " " << rnode->word << " : " << rnode->meaning << endl;
      postorder_rec (rnode->left);
    }
}

void
dictionary::create ()
{
  int n;
  string wordI, meaningI;
  cout << "\nHow many Word to insert?:\n";
  cin >> n;
  for (int i = 0; i < n; i++)
    {
      cout << "\nENter Word: ";
      cin >> wordI;
      cout << "\nEnter Meaning: ";
      cin >> meaningI;
      insert (wordI, meaningI);
    }
}

void
dictionary::inorder_rec (node * rnode)
{
  if (rnode)
    {
      inorder_rec (rnode->left);
      cout << " " << rnode->word << " : " << rnode->meaning << endl;
      inorder_rec (rnode->right);
    }
}

bool
dictionary::insert (string word, string meaning)
{
  node *p = new node (word, meaning);
  if (root == NULL)
    {
      root = p;
      return true;
    }
  node *cur = root;
  node *par = root;
  while (cur != NULL)		//traversal
    {
      if (word > cur->word)
	{
	  par = cur;
	  cur = cur->right;
	}
      else if (word < cur->word)
	{
	  par = cur;
	  cur = cur->left;
	}
      else
	{
	  cout << "\nWord is already in the dictionary.";
	  return false;
	}
    }
  if (word > par->word)		//insertion of node
    {
      par->right = p;
      return true;
    }
  else
    {
      par->left = p;

      return true;
    }
}

int
main ()
{
  string word;
  dictionary months;
  months.create ();
  cout << "Ascending order\n";
  months.inorder ();

  cout << "\nDescending order:\n";
  months.postorder ();

  cout << "\nEnter word to search: ";
  cin >> word;
  int comparisons = months.search (word);
  if (comparisons == -1)
    {
      cout << "\nNot found word";
    }
  else
    {
      cout << "\n " << word << " found in " << comparisons << " comparisons";
    }
  return 0;
}

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  #include <iostream>
#include <queue>
using namespace std;

int adj_mat[50][50] = { 0, 0 };
int visited[50] = { 0 };

void
dfs (int s, int n, string arr[])
{
  visited[s] = 1;
  cout << arr[s] << " ";
  for (int i = 0; i < n; i++)
    {
      if (adj_mat[s][i] && !visited[i])
	dfs (i, n, arr);
    }
}

void
bfs (int s, int n, string arr[])
{
  bool visited[n];
  for (int i = 0; i < n; i++)
    visited[i] = false;
  int v;
  queue < int >bfsq;
  if (!visited[s])
    {
      cout << arr[s] << " ";
      bfsq.push (s);
      visited[s] = true;
      while (!bfsq.empty ())
	{
	  v = bfsq.front ();
	  for (int i = 0; i < n; i++)
	    {
	      if (adj_mat[v][i] && !visited[i])
		{
		  cout << arr[i] << " ";
		  visited[i] = true;
		  bfsq.push (i);
		}
	    }
	  bfsq.pop ();
	}
    }
}

int
main ()
{
  cout << "Enter no. of cities: ";
  int n, u;
  cin >> n;
  string cities[n];
  for (int i = 0; i < n; i++)
    {
      cout << "Enter city #" << i << " (Airport Code): ";
      cin >> cities[i];
    }

  cout << "\nYour cities are: " << endl;
  for (int i = 0; i < n; i++)
    cout << "city #" << i << ": " << cities[i] << endl;
  for (int i = 0; i < n; i++)
    {
      for (int j = i + 1; j < n; j++)
	{
	  cout << "Enter distance between " << cities[i] << " and " <<
	    cities[j] << " : ";
	  cin >> adj_mat[i][j];
	  adj_mat[j][i] = adj_mat[i][j];
	}
    }
  cout << endl;
  for (int i = 0; i < n; i++)
    cout << "\t" << cities[i] << "\t";
  for (int i = 0; i < n; i++)
    {
      cout << "\n" << cities[i];
      for (int j = 0; j < n; j++)
	cout << "\t" << adj_mat[i][j] << "\t";
      cout << endl;
    }
  cout << "Enter Starting Vertex: ";
  cin >> u;
  cout << "DFS: ";
  dfs (u, n, cities);
  cout << endl;
  cout << "BFS: ";
  bfs (u, n, cities);
  return 0;
}

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  /*

Group C: Experiment 13
Adjacency Matrix : using adj matrix -BFS(Que)

*/

#include <iostream>
#include <stdlib.h>
using namespace std;

int cost[10][10], i, j, k, n, qu[10], front, rear, v, visit[10], visited[10];
int stk[10], top, visit1[10], visited1[10];

int main()
{
    int m;
    cout << "Enter number of vertices : ";
    cin >> n;
    cout << "Enter number of edges : ";
    cin >> m;
    
    cout << "\nEDGES :\n";
    for (k = 1; k <= m; k++)
    {
        cin >> i >> j;
        cost[i][j] = 1;
        cost[j][i] = 1;
    }
    
    //display function
    cout << "The adjacency matrix of the graph is : " << endl;
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
        {
            cout << " " << cost[i][j];
        }
        cout << endl;
    }
    
    cout << "Enter initial vertex : ";
    cin >> v;
    cout << "The BFS of the Graph is\n";
    cout << v<<endl;
    visited[v] = 1;
    k = 1;
    while (k < n)
    {
        for (j = 1; j <= n; j++)
            if (cost[v][j] != 0 && visited[j] != 1 && visit[j] != 1)
            {
                visit[j] = 1;
                qu[rear++] = j;
            }
        v = qu[front++];
        cout << v << " ";
        k++;
        visit[v] = 0;
        visited[v] = 1;
    }
    
    cout <<endl<<"Enter initial vertex : ";
    cin >> v;
    cout << "The DFS of the Graph is\n";
    cout << v<<endl;
    visited[v] = 1;
    k = 1;
    while (k < n)
    {
        for (j = n; j >= 1; j--)
            if (cost[v][j] != 0 && visited1[j] != 1 && visit1[j] != 1)
            {
                visit1[j] = 1;
                stk[top] = j;
                top++;
            }
        v = stk[--top];
        cout << v << " ";
        k++;
        visit1[v] = 0;
        visited1[v] = 1;
    }

    return 0;
}

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  /*

Group C: Experiment 13 
Adjecency List

*/

#include <iostream>
using namespace std;
#define MAX 10
#define TRUE 1
#define FALSE 0

// declaring an adjacency list for storing the graph
class lgra
{
private:
    struct node1
    {
        int vertex;
        struct node1 *next;
    };
    node1 *head[MAX];
    int visited[MAX];

public:
    //static int nodecount;
    lgra();
    void create();
    void dfs(int);
};

//constructor
lgra::lgra()
{
    int v1;
    for (v1 = 0; v1 < MAX; v1++)
        visited[v1] = FALSE;
    for (v1 = 0; v1 < MAX; v1++)
        head[v1] = NULL;
}

void lgra::create()
{
    int v1, v2;
    char ans;
    node1 *N, *first;
    cout << "Enter the vertices no. beginning with 0 : ";
    do
    {
        cout << "\nEnter the Edge of a graph : \n";
        cin >> v1 >> v2;
        if (v1 >= MAX || v2 >= MAX)
            cout << "Invalid Vertex Value!!\n";
        else
        {
            //creating link from v1 to v2
            N = new node1;
            if (N == NULL)
                cout << "Insufficient Memory!!\n";
            N->vertex = v2;
            N->next = NULL;
            first = head[v1];
            if (first == NULL)
                head[v1] = N;
            else
            {
                while (first->next != NULL)
                    first = first->next;
                first->next = N;
            }
            //creating link from v2 to v1
            N = new node1;
            if (N == NULL)
                cout << "Insufficient Memory!!\n";
            N->vertex = v1;
            N->next = NULL;
            first = head[v2];
            if (first == NULL)
                head[v2] = N;
            else
            {
                while (first->next != NULL)
                    first = first->next;
                first->next = N;
            }
        }
        cout << "\n Want to add more edges?(y/n) : ";
        cin >> ans;
    } while (ans == 'y');
}

//dfs function
void lgra::dfs(int v1)
{
    node1 *first;
    cout << endl
         << v1;
    visited[v1] = TRUE;
    first = head[v1];
    while (first != NULL)
        if (visited[first->vertex] == FALSE)
            dfs(first->vertex);
        else
            first = first->next;
}

int main()
{
    int v1;
    lgra g;
    
    g.create();
    cout << endl << "Enter the vertex from where you want to traverse : ";
    cin >> v1;
    if (v1 >= MAX)
        cout << "Invalid Vertex!!\n";
    else
    {
        cout << "The Dfs of the graph : ";
        g.dfs(v1);
    }
    
    return 0;
}

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  #include <iostream>
#include<string>
using namespace std;

class dictionary;
class node
{
  string word, meaning;
  node *left, *right;
public:
    friend class dictionary;
    node ()
  {
    left = NULL;
    right = NULL;

  }
  node (string word, string meaning)
  {
    this->word = word;
    this->meaning = meaning;
    left = NULL;
    right = NULL;
  }
};

class dictionary
{
  node *root;
public:
    dictionary ()
  {
    root = NULL;
  }
  void create ();
  void inorder_rec (node * rnode);
  void postorder_rec (node * rnode);
  void inorder ()
  {
    inorder_rec (root);
  }
  void postorder ();

  bool insert (string word, string meaning);
  int search (string key);

};

int
dictionary::search (string key)
{
  node *tmp = root;
  int count;
  if (tmp == NULL)
    {
      return -1;
    }
  if (root->word == key)
    return 1;
  while (tmp != NULL)
    {

      if ((tmp->word) > key)
	{
	  tmp = tmp->left;
	  count++;
	}
      else if ((tmp->word) < key)
	{
	  tmp = tmp->right;
	  count++;
	}
      else if (tmp->word == key)
	{
	  return ++count;
	}
    }
  return -1;

}

void
dictionary::postorder ()
{
  postorder_rec (root);
}

void
dictionary::postorder_rec (node * rnode)
{
  if (rnode)
    {
      postorder_rec (rnode->right);
      cout << " " << rnode->word << " : " << rnode->meaning << endl;
      postorder_rec (rnode->left);
    }
}

void
dictionary::create ()
{
  int n;
  string wordI, meaningI;
  cout << "\nHow many Word to insert?:\n";
  cin >> n;
  for (int i = 0; i < n; i++)
    {
      cout << "\nENter Word: ";
      cin >> wordI;
      cout << "\nEnter Meaning: ";
      cin >> meaningI;
      insert (wordI, meaningI);
    }
}

void
dictionary::inorder_rec (node * rnode)
{
  if (rnode)
    {
      inorder_rec (rnode->left);
      cout << " " << rnode->word << " : " << rnode->meaning << endl;
      inorder_rec (rnode->right);
    }
}

bool
dictionary::insert (string word, string meaning)
{
  node *p = new node (word, meaning);
  if (root == NULL)
    {
      root = p;
      return true;
    }
  node *cur = root;
  node *par = root;
  while (cur != NULL)		//traversal
    {
      if (word > cur->word)
	{
	  par = cur;
	  cur = cur->right;
	}
      else if (word < cur->word)
	{
	  par = cur;
	  cur = cur->left;
	}
      else
	{
	  cout << "\nWord is already in the dictionary.";
	  return false;
	}
    }
  if (word > par->word)		//insertion of node
    {
      par->right = p;
      return true;
    }
  else
    {
      par->left = p;

      return true;
    }
}

int
main ()
{
  string word;
  dictionary months;
  months.create ();
  cout << "Ascending order\n";
  months.inorder ();

  cout << "\nDescending order:\n";
  months.postorder ();

  cout << "\nEnter word to search: ";
  cin >> word;
  int comparisons = months.search (word);
  if (comparisons == -1)
    {
      cout << "\nNot found word";
    }
  else
    {
      cout << "\n " << word << " found in " << comparisons << " comparisons";
    }
  return 0;
}

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  #include<iostream>
#include<math.h>
using namespace std;

struct Bstnode
{
     int data;
     Bstnode *left = NULL;
     Bstnode *right = NULL;
 
};

class Btree
{
 
      int n;
      int x;
      int flag;
  
      public:
      Bstnode * root;
      Btree()
      {
         root = NULL;
      }
 
 Bstnode *GetNewNode(int in_data)
 {
      Bstnode * ptr = new Bstnode();
      ptr->data = in_data;
      ptr->left = NULL;
      ptr->right = NULL;
      return ptr;
 }
 
 Bstnode *insert( Bstnode *temp , int in_data)
 {
      if( temp == NULL )
          {
             temp = GetNewNode(in_data);
          }
      else if( temp->data > in_data)
          {
             temp->left = insert(temp->left , in_data);
          }
      else
          {
             temp->right = insert( temp->right , in_data);
          }
      return temp;
 }
 
 void input()
{
      cout<<"ENTER NUMBER OF ELEMENTS IN THE BST : ";
      cin>>n;
      for(int i = 0 ; i < n ; i++)
      {
           cout<<"NUMBER = ";
           cin>>x;
           root = insert(root , x);
      }
}
 
int search(Bstnode *temp ,int in_data)
{
    if( temp != NULL)
      {
        if(temp->data == in_data)
           {
                cout<<":-- RECORD FOUND --:"<<endl;
                return 1;
           }
        else if(in_data < temp->data)
           {
                this->search(temp->left, in_data);
           }
        else if(in_data > temp->data)
           {
                this->search(temp->left , in_data);
           }
      }
      else
      {
        return 0;
      }
}
 
 
void minvalue(Bstnode *temp)
{
     while(temp->left != NULL)
      {
         temp = temp->left;
      }
      cout<<"MINIMUM VALUE = "<<temp->data<<endl;
}
   
void mirror(Bstnode *temp)
{
    if(temp == NULL)
      {
         return;
      }
    else
    {
       Bstnode *ptr;
       mirror(temp->left);
       mirror(temp->right);
       ptr = temp->left;
       temp->left = temp->right;
       temp->right = ptr; 
    }
}
 
void display()
{
      cout<<endl<<"--- INORDER TRAVERSAL ---"<<endl;
      inorder(root);
      cout<<endl;
      cout<<endl<<"--- POSTORDER TRAVERSAL ---"<<endl;
      postorder(root);
      cout<<endl;
      cout<<endl<<"--- PREORDER TRAVERSAL ---"<<endl;
      preorder(root);
      cout<<endl;
  
}
 
void inorder(Bstnode *temp)
{
    if(temp != NULL)
    {
       inorder(temp->left);
       cout<<temp->data<<"  ";
       inorder(temp->right);
    }
} 
 
void postorder(Bstnode *temp)
    {
        if(temp != NULL)
            {
               postorder(temp->left);
               postorder(temp->right);
               cout<<temp->data<<" ";
            }
}
 
void preorder(Bstnode *temp)
{
    if(temp != NULL)
    {
       cout<<temp->data<<" ";
       preorder(temp->left);
       preorder(temp->right);
    }
} 
 
int depth(Bstnode *temp)
{
      if(temp == NULL) 
       return 0;
      return (max((depth(temp->left)),(depth(temp->right))) +1);  
}
};

int main()
{
     Btree obj;
     obj.input();
     obj.display();
     int a = 0;
     a = obj.search(obj.root,10);
     if( a == 0)
         {
          cout<<"ELEMENT NOT FOUND"<<endl;
         }
         else
          cout<<"ELEMENT FOUND"<<endl;
         cout<<endl<<a<<endl;
         obj.minvalue(obj.root);
         obj.mirror(obj.root);
         obj.inorder(obj.root);
         //int d ;
         cout<<endl<<obj.depth(obj.root);
         //cout<<endl<<d<<endl;
         return 0;
}

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  #include<iostream>
#include<stdlib.h>
#include<string.h>
using namespace std;
struct node
{   char name[20];
     node *next;
     node *down;
      int flag;
};
class Gll
{   char ch[20];    int n,i;    
     node *head=NULL,*temp=NULL,*t1=NULL,*t2=NULL;
     public:
     node *create();
     void insertb();
     void insertc();
     void inserts();
     void insertss();
     void displayb();
    
};
node *Gll::create()
{
    node *p=new(struct node);
    p->next=NULL;
    p->down=NULL;
    p->flag=0;
    cout<<"\n enter the name";
    cin>>p->name;
    return p;
}
void Gll::insertb()
{      
        
         if(head==NULL)
           {    t1=create();
                head=t1;
           }
           else
           {
              cout<<"\n book exist";
           }   
}     
void Gll::insertc()
{     
      if(head==NULL)
          { 
                  cout<<"\n there is no book";   
           }
           else
           {    cout<<"\n how many chapters you want to insert";
                cin>>n;
                for(i=0;i<n;i++)
                {
                t1=create();
                if(head->flag==0)
                {  head->down=t1;   head->flag=1;    }
                else
                {   temp=head;
                     temp=temp->down;
                    while(temp->next!=NULL)
                         temp=temp->next;
                     temp->next=t1;
                }
                }
          }
                    
                              
} 
void Gll::inserts()
{     
  
         if(head==NULL)
          { 
                  cout<<"\n there is no book";   
           }
           else
           {    cout<<"\n Enter the name of chapter on which  you want to enter the section";
                 cin>>ch;
                
                 temp=head;
               if(temp->flag==0)
               {   cout<<"\n their are no chapters on in book";
               }
               else
               {    temp=temp->down;
                while(temp!=NULL)
                 { 
                      if(!strcmp(ch,temp->name))
                      {   
                                cout<<"\n how many sections you want to enter";
                                cin>>n;
                                for(i=0;i<n;i++)
                                {
                                   
                                           t1=create();
                                               if(temp->flag==0)
                                               {      temp->down=t1;
                                                     
                                                        temp->flag=1;  cout<<"\n******";
                                                        t2=temp->down;
                                                   
                                               }
                                              else
                                               {           
                                                              cout<<"\n#####";
                                                               while(t2->next!=NULL)
                                                               {     t2=t2->next;          }
                                                                       t2->next=t1;                 
                                                 }   
                                 }                              
                                   break;       
                       }  
                               temp=temp->next;
                  }
                }    
         }
}
void Gll::insertss()
{     
  
         if(head==NULL)
          { 
                  cout<<"\n there is no book";   
           }
           else
           {    cout<<"\n Enter the name of chapter on which  you want to enter the section";
                 cin>>ch;
                
                 temp=head;
               if(temp->flag==0)
               {   cout<<"\n their are no chapters on in book";
               }
               else
               {    temp=temp->down;
                while(temp!=NULL)
                 { 
                      if(!strcmp(ch,temp->name))
                      {       
                         cout<<"\n enter name of section in which you want to enter the sub section";
                         cin>>ch;
                        
                        if(temp->flag==0)
                        {   cout<<"\n their are no sections ";   }
                         else
                         {       temp=temp->down;
                                 while(temp!=NULL)
                                 {
                                     if(!strcmp(ch,temp->name))
                                     {
                                      cout<<"\n how many subsections you want to enter";
                                        cin>>n;
                    for(i=0;i<n;i++)
                                   {
                                   
                                           t1=create();
                                               if(temp->flag==0)
                                               {      temp->down=t1;
                                                     
                                                        temp->flag=1;  cout<<"\n******";
                                                        t2=temp->down;
                                                   
                                               }
                                              else
                                               {           
                                                              cout<<"\n#####";
                                                               while(t2->next!=NULL)
                                                               {     t2=t2->next;          }
                                                                       t2->next=t1;                 
                                                 }   
                                        }                              
                                         break;
                                     }      temp=temp->next;
                                   }
                          }       
                       }
                         
                               temp=temp->next;
                  }
                }    
         }
} 
void Gll::displayb()
{       
               
                if(head==NULL)
                {  cout<<"\n book not exist"; 
                }
                else
                {
                 temp=head;
                 
                    cout<<"\n NAME OF BOOK:  "<<temp->name;
                         if(temp->flag==1)
                         {
                         temp=temp->down;
                        
                           while(temp!=NULL)
                           {     cout<<"\n\t\tNAME OF CHAPTER:  "<<temp->name;
                                 t1=temp;
                                 if(t1->flag==1)
                                 {  t1=t1->down;
                                    while(t1!=NULL)
                                    {     cout<<"\n\t\t\t\tNAME OF SECTION:  "<<t1->name;
                                          t2=t1;
                                          if(t2->flag==1)
                                          {  t2=t2->down;
                                          while(t2!=NULL)
                                          {     cout<<"\n\t\t\t\t\t\tNAME OF SUBSECTION:  "<<t2->name;     
                                          t2=t2->next;
                                          }
                                          }     
                                          t1=t1->next;
                                    }
                                 }   
                                  temp=temp->next;
                           }
                        
                          }
                }         
                     
                  
                  
}                  
int main()
{    Gll g;   int x;  
       while(1)
      {    cout<<"\n\n enter your choice";
            cout<<"\n 1.insert book";
            cout<<"\n 2.insert chapter";
            cout<<"\n 3.insert section";
            cout<<"\n 4.insert subsection";
            cout<<"\n 5.display book";
            cout<<"\n 6.exit";
            cin>>x;
           switch(x)
           {   case 1:          g.insertb();
                                         break;             
                case 2:          g.insertc();
                                         break;      
                case 3:          g.inserts();
                                         break;
                case 4:          g.insertss();
                                         break;    
                case 5:          g.displayb();
                                         break;      
                case 6:  exit(0);
           }
       }
       return 0;
}

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  #include <iostream>
using namespace std;

const int MAX=100;
class dictionary;
class node
{
    string key,value;
    node *next;
    public:
        friend class dictionary;
        node()
        {
            next=NULL;
        }
        node(string key,string value)
        {
            this->key=key;
            this->value=value;
            next=NULL;
        }
};

class dictionary
{
    node *head[MAX];
    public:
    dictionary()
    {
        for(int i=0;i<MAX;i++)
        head[i]=NULL;
    }
    
    int hashf(string word);
    bool insert(string,string);
    string find(string word);
    bool deleteWord(string word);
};
bool dictionary::deleteWord(string word)
{
    int index=hashf(word);
    node *tmp=head[index];
    node *par=head[index];
    if(tmp==NULL) //if no word is present at that index
    {
        return false;
    }
    if(tmp->key==word && tmp->next==NULL)//only one word is present
    {
        tmp->next=NULL;
        delete tmp;
        return true;
    }
     //tmp=tmp->next;
    while(tmp->key!=word && tmp->next!=NULL)
    {
        par=tmp;
        tmp=tmp->next;
    }
    if(tmp->key==word&&tmp->next!=NULL)
    {
        par->next=tmp->next;
        tmp->next=NULL;
        delete tmp;
        return true;
    }
    else //delete at end
    {
        par->next=NULL;
        tmp->next=NULL;
        delete tmp;
        return true;
    }
    return false;
}

string dictionary::find(string word)
{
    int index=hashf(word);
    //cout<<"\nIndex in find"<<index;
    node *start=head[index];
    if(start==NULL)
    return "-1";
    while(start!=NULL)
    {
        if(start->key==word)
        return start->value;
        start=start->next;
    }
    return "-1";
    }
    
    bool dictionary::insert(string word,string meaning)
    {
        int index=hashf(word);
        node *p=new node(word,meaning);

    if(head[index]==NULL)
    {
        head[index]=p;
        cout<<"\n"<<word<<"inserted. ";
        return true;
    }
    else
    {
        node *start=head[index];
        while(start->next!=NULL)
        start=start->next;

        start->next=p;
        cout<<"\n"<<word<<"inserted. ";
        return true;
    }
    return false;
}

int dictionary::hashf(string word)
{
    int asciiSum=0;
    for(int i=0;i<word.length();i++)
    {
        asciiSum=asciiSum+word[i];
    }
    return (asciiSum%100);
}

int main() 
{
    dictionary oxford;
    int choice;
    string word,meaning;
    do
    {
        cout<<"\n**** OXFORD DICTIONARY ****\n"
        <<"1.Insert Word\n"
        <<"2.Find Word\n"
        <<"3.Delete Word\n"
        <<"Enter Your Choice :";
        cin>>choice;
        switch(choice)
        {
           case 1:
           cout<<"Enter Word: ";
           cin>>word;
           cout<<"Enter Meaning: ";
           cin>>meaning;
           if(oxford.insert(word,meaning))
           cout<<endl<<word<<" inserted into dictionary.";
           else
           cout<<"\nFailed to insert.";
           break;
           
           case 2:
           cout<<"Enter Word to Search: ";
           cin>>word;
           meaning=oxford.find(word);
           if(meaning!="-1")
                cout<<" Word Is present.\n"<<word<<" = "<<meaning ;
           else
           {
                cout<<"\n Word Not Present";
           }
           break;
           
           case 3:
           cout<<"Enter Word to Delete: ";
           cin>>word;
           if(oxford.deleteWord(word))
           cout<<" Word is deleted.";
           else
           {
                cout<<"\nFailed to delete "<<word;
           }
           break;
           default:
                cout<<"\nWrong Choice.";
    }

 }
 
 while(choice!=0);

 return 0;
}

          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
    
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
           #include<iostream>
 #include<cstdlib>
 #include<string>
 #include<cstdio>
 using namespace std;
 const int TABLE_SIZE = 128;

 class HashEntry
 {
	 public:
 	 int key;
 	 int value;
	 HashEntry(int key, int value)
	 {
 		this->key = key;
		this->value = value;
 	 }
 };

 class HashMap
 {
 	private:
 	HashEntry **table;
 	public:
 	HashMap()
 	{
 		table = new HashEntry * [TABLE_SIZE];
 		for (int i = 0; i< TABLE_SIZE; i++)
 		{
 			table[i] = NULL;
 		}
 	}
	
 int HashFunc(int key)
 {
 	return key % TABLE_SIZE;
 }
 
 void Insert(int key, int value)
 {
 	int hash = HashFunc(key);
 	while (table[hash] != NULL && table[hash]->key != key)
 	{
 		hash = HashFunc(hash + 1);
 	}
 	if (table[hash] != NULL)
	delete table[hash];
 	table[hash] = new HashEntry(key, value);
 }
 
 int Search(int key)
 {
 	int hash = HashFunc(key);
 	while (table[hash] != NULL && table[hash]->key != key)
 	{
 		hash = HashFunc(hash + 1);
 	}
	
 	if (table[hash] == NULL)
 	return -1;
 	else
	return table[hash]->value;
 }

 void Remove(int key)
 {
 	int hash = HashFunc(key);
 	while (table[hash] != NULL)
 	{
 		if (table[hash]->key == key)
	 break;
 	 hash = HashFunc(hash + 1);
 	}
 	if (table[hash] == NULL)
 	{
 		cout<<"No Element found at key "<<key<<endl;
		return;
	}
	else
 	{
 		delete table[hash];
 	}
 		cout<<"Element Deleted"<<endl;
 }
 
 ~HashMap()
 {
 	for (int i = 0; i < TABLE_SIZE; i++)
	{
 		if (table[i] != NULL)
 		delete table[i];
	 	delete[] table;
 	}
 }
 };
 
 int main()
 {
 	HashMap hash;
 	int key, value;
 	int choice;
	while (1)
	{
 		cout<<"\n----------------------"<<endl;
 		cout<<"Operations on Hash Table"<<endl;
 		cout<<"\n----------------------"<<endl;
 		cout<<"1.Insert element into the table"<<endl;
 		cout<<"2.Search element from the key"<<endl;
 		cout<<"3.Delete element at a key"<<endl;
		cout<<"4.Exit"<<endl;
 		cout<<"Enter your choice: ";
 		cin>>choice;
		
 		switch(choice)
 			{
				 case 1:
 				 cout<<"Enter element to be inserted: ";
 				 cin>>value;
				 cout<<"Enter key at which element to be inserted: ";
				 cin>>key;
				 hash.Insert(key, value);
				 break;
				 
				 case 2:
				 cout<<"Enter key of the element to be searched: ";
				 cin>>key;
				 
				 if (hash.Search(key) == -1)
 				 {
 	 				cout<<"No element found at key "<<key<<endl;
 					continue;
				 }
				 else
 				 {
					 cout<<"Element at key "<<key<<" : ";
					 cout<<hash.Search(key)<<endl;
				 }
 				 break;
 				
				 case 3:
				 cout<<"Enter key of the element to be deleted: ";
				 cin>>key;
				 hash.Remove(key);
				 break;
				 
 				 case 4:
				 exit(1);
				 
				 default:
				 cout<<"\nEnter correct option\n";
			}
	 }
 	 return 0;
 }

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
