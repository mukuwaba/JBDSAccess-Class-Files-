import java.sql.*;
import java.util.Scanner;

public class JDBCMSAccess {
    public static void main(String[] args) throws SQLException {// m + TAB

        //Create a reference to the Connection object, which allows us to red/write to the DBMS
        Connection con = DriverManager.getConnection("jdbc:ucanaccess://C:/Users/mukuwa.baffoe/MB.accdb");
        //MB is the name of my Access database and .accdb is the file extension
        //Make sure the file path define above is correct
        //To check go to External Libraries and enter the path that the database is under, use path above
        // In database tools, click Compact and Repair --> clears bugs and errors
        //Create a reference to the STATEMENT object, which allows us to EXECUTE a SQL statement/query
        Statement st = con.createStatement();

        //////Optional Code///////
        // Scanner stringScanner = new Scanner(System.in);
        // String useInput = stringScanner.next();
        //how you do a sequal injection
        ////////////////////////

        ResultSet rs = st.executeQuery("Select * FROM Student");
        //Select * From Student --> hard code
        //Make sure the table within Access is named Student
        //The program will pull information within this table
        //Can change between tables

        //Get header row information
        ResultSetMetaData rsmd = rs.getMetaData();
        //The metadata of a table is information about the table itself. How many columns, etc.
        //rsmd- result set metadata
        int numberOfColumns = rsmd.getColumnCount();
        //gets the number of columns from Acccess database


        //Print the header row, per se.
        //for(int count =1; count <= numberColumns; count++) {
         //   System.out.printf("%s\t", rsmd.getColumnName(count));
        //}
         //   System.out.println();


        //Add a header row for the output report

        for (int colCount = 1; colCount <= numberOfColumns; colCount++){
            System.out.printf("%-10s", rsmd.getColumnName(colCount));
        }//End: for

        System.out.println();

        //Loop through each row and print the table
        while (rs.next()) {
           // System.out.println(rs.getString(1)+"\t" +rs.getString(2) +"\t" + rs.getString(3) + "\n");
            System.out.printf("%-10s%-10s%-10s%n",
            rs.getString(1), rs.getString(2), rs.getString(3));

            //Prints the data entries within the database
        }//End: While
        //VITAL: Close the connection / close off open items
        rs.close();
        st.close();
        con.close();

    }//End:main
}//End:class
