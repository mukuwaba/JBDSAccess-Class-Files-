import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class JDBCAccessTest {//inserts a row into the database defined in the path address
    public static void main(String[] args) throws SQLException {//m+TAB

        String databaseURL = "jdbc:ucanaccess://C:/Users/mukuwa.baffoe/MB3.accdb";
        try (Connection connection = DriverManager.getConnection(databaseURL)) {//error handing--> try some code
            String sql = "INSERT INTO STUDENT (FirstName, LastName) Values (?, ?)";
            //dont need ID because its an auto insert
            //each question mark for values
            PreparedStatement preparedStatement = connection.prepareStatement(sql);
            //sequal statement to do an insert into a table
            //starting to put a statment that we are going to execute

            preparedStatement.setString(1, "Timothy" );//ID column
            preparedStatement.setString(2,"ned@yahoo.com");
            int row = preparedStatement.executeUpdate();
            if (row > 0){
                System.out.println("A row has been inserted");
            }
            preparedStatement.close();
            //connection close;

                    //insert statement that adds a row to a database table
        } catch (SQLException ex) {//catch--> for if the code fails, will execute this line of code
            ex.printStackTrace();
        }//end catch
    }//End: main
}//End: class
