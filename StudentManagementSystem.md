
package studentmanagementsystem;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.sql.SQLException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

public class StudentManagementSystem 
{
       String sName,sCourse,yearAdmin;
        int age,adminNO,sID;
        long phoneNO;
       String sname;
       float MM,ME,MS,MSST,totalMarks,percentage;          
       
    public void EnterDetails()throws IOException,SQLException 
    { 
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        
        System.out.print("Enter Admisson Number     :");
        adminNO=Integer.parseInt(br.readLine());
        System.out.print("Enter Student name        :");
        sName=br.readLine();
        System.out.print("Enter Standard of Student :");
        sCourse=br.readLine();
        System.out.print("Enter Age of student      :");
        age=Integer.parseInt(br.readLine());
        System.out.print("Enter phone number        :");
        phoneNO=Long.parseLong(br.readLine());
        System.out.print("Year of Admission         :");
        yearAdmin=br.readLine();
        String uri="jdbc:derby://localhost:1527/StudentManagementSystem";
        String uid="app";
        String pass="app";
        Connection conn=DriverManager.getConnection(uri,uid,pass);
        PreparedStatement stat=conn.prepareStatement("insert into Student_Management values(?,?,?,?,?,?)");
        
        stat.setInt(1,adminNO);
        stat.setString(2,sName);
        stat.setString(3,sCourse);
        stat.setInt(4,age);
        stat.setLong(5,phoneNO);
        stat.setString(6,yearAdmin);
        stat.executeUpdate();
        System.out.println("Your data saved successfully");
    }
    public void ViewAllRecords() throws IOException,SQLException
    {
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        String uri="jdbc:derby://localhost:1527/StudentManagementSystem";
        String uid="app";
        String pass="app";
        Connection conn=DriverManager.getConnection(uri,uid,pass);
        PreparedStatement stat=conn.prepareStatement("Select * from Student_Management");
        ResultSet rs=stat.executeQuery();
        System.out.println("Admission_No \t Student_Name \t Standard \t Student_Age \t Phone_no \t Year_Admission");
    while(rs.next())
        {
          System.out.println(rs.getString(1)+"\t"+rs.getString(2)+"\t"+rs.getString(3)+"\t"+rs.getString(4)+"\t"+rs.getString(5)+"\t"+rs.getString(6));
        }
    }    
    public void CeckDetails() throws IOException,SQLException
    {
         BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        System.out.print("Enter Admisson Number     :");
        adminNO=Integer.parseInt(br.readLine());
        String uri="jdbc:derby://localhost:1527/StudentManagementSystem";
        String uid="app";
        String pass="app";
        Connection conn=DriverManager.getConnection(uri,uid,pass);
        PreparedStatement stat=conn.prepareStatement("Select * from Student_Management where Admission_NO=?");
        stat.setInt(1,adminNO);
        ResultSet rs=stat.executeQuery();
        System.out.println("ID \t Admission_No \t Student_Name \t Standard \t Student_Age \t Phone_no \t Year_Admission");
    while(rs.next())
        {
          System.out.println(rs.getString(1)+"\t"+rs.getString(2)+"\t"+rs.getString(3)+"\t"+rs.getString(4)+"\t"+rs.getString(5)+"\t"+rs.getString(6));
        }
    }

    public void UpdatePresonalInfo()throws IOException, SQLException 
    {
       
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        System.out.println("For change in name :1 ");
        System.out.println("For change in Phone number :2 ");
        System.out.println("Enter the option ");
        int n=Integer.parseInt(br.readLine());
        System.out.print("Enter Admisson Number     :");
        adminNO=Integer.parseInt(br.readLine());
        
        switch(n)
        {
            case 1:
            {
                System.out.print("Enter Student name        :");
            sName=br.readLine();
            String uri="jdbc:derby://localhost:1527/StudentManagementSystem";
            String uid="app";
            String pass="app";
            Connection conn=DriverManager.getConnection(uri,uid,pass);
            PreparedStatement stat=conn.prepareStatement("update Student_Management set Student_Name=? where Admission_NO=?");
            stat.setInt(2,adminNO);
            stat.setString(1,sName);
                stat.executeUpdate();

       
                break;
            }
            case 2:
            {
                System.out.print("Enter phone number        :");
            phoneNO=Integer.parseInt(br.readLine());
            String uri="jdbc:derby://localhost:1527/StudentManagementSystem";
            String uid="app";
            String pass="app";
            Connection conn=DriverManager.getConnection(uri,uid,pass);
            PreparedStatement stat=conn.prepareStatement("update Student_Management set Phone_NO=? where Admission_NO=?");
            stat.setInt(2,adminNO);
            stat.setLong(1,phoneNO);
                stat.executeUpdate();

                break;
            }
        
                default :
           {
           System.out.println("thank u");
           break;
           }
        
        
       
        
        }
        
           System.out.println("Record updated");

        
    }

    public void MarksEntery() throws IOException,SQLException
    {
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        
        System.out.print("Enter Admission Number              :");
        sID=Integer.parseInt(br.readLine());
        System.out.print("Enter Student Name                  :");
        sname=br.readLine();
        System.out.print("Marks in Marks out of 100           :");
        MM=Float.parseFloat(br.readLine());
        System.out.print("Marks in English out of 100         :");
        ME=Float.parseFloat(br.readLine());
        System.out.print("Marks in Science out of 100         :");
        MS=Float.parseFloat(br.readLine());
        System.out.print("Marks in Social Science out of 100  :");
        MSST=Float.parseFloat(br.readLine());
        totalMarks=MM+ME+MS+MSST;
        System.out.println("Total Marks out of 400 are          :"+totalMarks);
        percentage=totalMarks/4;
        System.out.print("Percentage of marks                 :"+percentage);
        String uri="jdbc:derby://localhost:1527/StudentManagementSystem";
        String uid="app";
        String pass="app";
        Connection conn=DriverManager.getConnection(uri,uid,pass);
        PreparedStatement stat=conn.prepareStatement("insert into Marks_Entry values(?,?,?,?,?,?,?,?)");
        stat.setInt(1,sID);
        stat.setString(2,sname);
        stat.setFloat(3,MM);
        stat.setFloat(4,ME);
        stat.setFloat(5,MS);
        stat.setFloat(6,MSST);
        stat.setFloat(7,totalMarks);
        stat.setFloat(8,percentage);
        stat.executeUpdate();
        System.out.println("Your data saved successfully");

    }

    public void ViewAcademicInfo() throws IOException,SQLException
    {
        BufferedReader c=new BufferedReader(new InputStreamReader(System.in));
        System.out.println("Enter Student ID");
        sID=Integer.parseInt(c.readLine());
        String uri="jdbc:derby://localhost:1527/StudentManagementSystem";
        String uid="app";
        String pass="app";
        Connection conn=DriverManager.getConnection(uri,uid,pass);
        PreparedStatement stat=conn.prepareStatement("Select * from Marks_Entry where Admission_NO=?");
        stat.setInt(1,sID);
         ResultSet rs=stat.executeQuery();
         System.out.println("Student ID\tStudent Name\tMaths\tEnglish\tScience\tSST\tTotal marks\tPercentage");
         while(rs.next())
         {
          System.out.println(rs.getString(1)+"\t"+rs.getString(2)+"\t"+rs.getString(3)+"\t"+rs.getString(4)+"\t"+rs.getString(5)+"\t"+rs.getString(6)+"\t"+rs.getString(7)+"\t"+rs.getString(8));
         }
    }
    
    public static void main(String[] args)throws IOException, SQLException
    {
     int n=0;
     StudentManagementSystem SMS=new StudentManagementSystem();
     while(n != 7)
     {
     BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
     System.out.println("");
     System.out.println("Enter Admission Details    :1");
     System.out.println("View All Records           :2");
     System.out.println("Check Details              :3");
     System.out.println("Update Personal Information:4");
     System.out.println("Marks Entry                :5");
     System.out.println("View Academic Information  :6");
     System.out.println("Exit                       :7");
     System.out.println("Enter the option ");
     n=Integer.parseInt(br.readLine());
    
      
     switch(n)
     {
         case 1:
         {
             SMS.EnterDetails();
             break;
         }
         case 2:
         {
             SMS.ViewAllRecords();
             break;
         }
         case 3:
         {
             SMS.CeckDetails();
             break;
         }
         case 4:
         {
             SMS.UpdatePresonalInfo();
             break;
         }
         case 5:
         {
             SMS.MarksEntery();
             break;
         }
         case 6:
         {
             SMS.ViewAcademicInfo();
             break;
         }
         case 7:
         {
             System.out.print("THANK YOU");
             break;
         }
     }
     }
    }
}
