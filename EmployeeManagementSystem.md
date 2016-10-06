#include<fstream.h>
#include<conio.h>
#include<stdio.h>
#include<string.h>
class trans
{
private:
int empid;
int srno;
float totalpay;
int month,year;
char tdate[50];
char ename[50];
public:
friend void report1();
int accept()
{
 cout<<endl<<"Enter Month";
 cin>>month;
 cout<<endl<<"Enter Year";
 cin>>year;
 cout<<"Enter today date";
 gets(tdate);
 cout<<endl<<"Enter emp id";
 cin>>empid;
 fstream rd;
 rd.open("emp.txt",ios::in);
 rd.seekg(0,ios::end);
 int n=rd.tellg()/sizeof(obj);
 rd.seekg(0,ios::beg);
 for(int i=1;i<=n;i++)
 {
  rd.read((char *)&obj,sizeof(obj));
  if(obj.empid==empid)
  {
   strcpy(ename,obj.name);
   totalpay=obj.bsal+obj.hra+obj.perks;
   cout<<endl<<"Name :"<<ename;
   cout<<endl<<"Basic salary: "<<obj.bsal;
   cout<<endl<<"House rental allowance: "<<obj.hra;
   cout<<endl<<"Perks : "<<obj.perks;
   cout<<endl<<"Total : "<<totalpay;
   fstream rd1;
   rd1.open("pay.txt",ios::in);
   rd1.seekg(0,ios::end);
   int tn=rd1.tellg()/sizeof(tobj);
   srno=tn+1;
   cout<<endl<<"Sr No "<<srno;
   return 1;
   break;
  }
 }
 return 0;
}
void display()
{
 cout<<srno<<"\t"<<ename<<"\t"<<totalpay<<"\t"<<tdate<<endl;
}
};
trans tobj;
class emp
{
 public:
 int empid;
 float bsal,hra,perks;
 char name[50],fname[50],doj[50];
 public:
 void accept()
 {
  cout<<endl<<"enter employee id";
  cin>>empid;
  cout<<"enter name";
  gets(name);
  cout<<"enter father name";
  gets(fname);
  cout<<"enter basic salary";
  cin>>bsal;
  cout<<"enter house rental allowance";
  cin>>hra;
  cout<<"enter perks ";
  cin>>perks;
 }
 void display()
 {
  cout<<endl<<"Employee ID "<<empid;
  cout<<endl<<"Employee name "<<name;
  cout<<endl<<"Father Name "<<fname;
  cout<<endl<<"Basic Salary "<<bsal;
  cout<<endl<<"House rental allowance "<<hra;
  cout<<endl<<"Perks "<<perks;
 }
};
emp obj;
void addemp()
{
 obj.accept();
 fstream wr;
 wr.open("emp.txt",ios::app);
 wr.write((char *)&obj,164);
 cout<<"Object written sucessfully";
}
void givepay()
{

 if(tobj.accept()==1)
 {
  fstream wr1;
  wr1.open("pay.txt",ios::app);
  wr1.write((char *)&tobj,sizeof(tobj));
  cout<<"Pay disbursed sucessfully";
 }
 else
 {
 cout<<"Invalid empid";
 }
}
void report1()
{
 int m,y;
 clrscr();
 cout<<endl<<"enter month";
 cin>>m;
 cout<<endl<<"enter year";
 cin>>y;
 fstream rd1;
 rd1.open("pay.txt",ios::in);
 rd1.seekg(0,ios::end);
 int n=rd1.tellg()/sizeof(tobj);
 rd1.seekg(0,ios::beg);
 for(int i=1;i<=n;i++)
 {
  rd1.read((char *)&tobj,sizeof(tobj));
  if(m==tobj.month && y==tobj.year)
  {
  tobj.display();
  }
 }
}
void main()
{
clrscr();
report1();
getch();
}




