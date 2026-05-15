protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException

 response.setContentType("text/html");
PrintWriter out response.getWriter();

String userId request.getParameter("userId");

String password request.getParameter("password");

//JDBC Connection

try {

Class.forName("com.mysql.cj.jdbc.Driver");

Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "root", "root");

Statement st conn.createStatement();

String query = "select * from user where userid= ""+userId+"' and password= ""+password+"'";


ResultSet rs = st.executeQuery(query);

if(rs.next()) {

out.print("<h1>"+userId+": Welcome to Home page</h1><br>");

out.print("<h1>Login Successfully!</h1><br>");


}else {

// the userId and password is not available in DB

out.print("<h1>"+userId+": please enter correct userId and Password</h1><br>");

out.print("<h1>Login Failed!</h1><br>");
 }


rs.close();

st.close();

conn.close();


} catch (ClassNotFoundException e) {

// TODO Auto-generated catch block

out.print("<h1>Login Failed! becouse of server exception</h1><br>");

e.printStackTrace();

} catch (SQLException e) {

// TODO Auto-generated catch block

out.print("<h1>Login Failed! becouse of server exception</h1><br>");
e.printStackTrace();
}
