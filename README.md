# Delphi__To__MS_SQL_Server

To connect a Delphi project to Microsoft SQL Server, you typically use the **FireDAC** framework, which is a robust and flexible database access library included in modern versions of Delphi. Here's a step-by-step guide:

---

### 1. **Prepare Your SQL Server**
- Ensure that the SQL Server is running and accessible.
- Create a database and a user account with sufficient permissions.
- Note down the connection details:
  - **Server Name/IP**
  - **Database Name**
  - **Username**
  - **Password**

---

### 2. **Set Up Delphi Environment**
Ensure that the FireDAC components are installed in your Delphi environment. If FireDAC is unavailable, you may need an alternative like **ADO** or a third-party library.

---

### 3. **Add FireDAC Components**
1. Open your Delphi project.
2. Add the following FireDAC components to your form or data module:
   - **TFDConnection**: For managing the connection to SQL Server.
   - **TFDQuery** or **TFDTable**: For executing queries or working with tables.

---

### 4. **Configure the Connection**
- **Double-click** the `TFDConnection` component to open the Connection Editor.
- Set the following properties:
  - **DriverID**: `MSSQL`
  - **Server**: Enter the SQL Server's name or IP address.
  - **Database**: Specify the database name.
  - **User_Name**: Provide the username.
  - **Password**: Enter the password.
  - **MSSQL Provider**: Set it to `prNative` for the best performance (native SQL Server driver).
  
  Example of a Connection String:
  ```
  DriverID=MSSQL;Server=127.0.0.1;Database=MyDatabase;User_Name=sa;Password=myPassword;
  ```

- Click **Test** to verify the connection.

---

### 5. **Use the Connection**
- Set the `Connection` property of any `TFDQuery` or `TFDTable` components to your `TFDConnection` instance.
- Use the `SQL` property of `TFDQuery` to define your SQL queries.
- Use `Active := True` to activate the query or table and fetch data.

---

### 6. **Handle Errors and Exceptions**
Wrap your code in try-except blocks to handle connection issues and ensure a robust application.

Example:
```delphi
try
  FDConnection1.Connected := True;
  ShowMessage('Connected successfully!');
except
  on E: Exception do
    ShowMessage('Connection failed: ' + E.Message);
end;
```

---

### 7. **Compile and Run**
- Compile your project and run it to test the connection.

---

### Example Code
```delphi
procedure TForm1.Button1Click(Sender: TObject);
begin
  FDConnection1.DriverName := 'MSSQL';
  FDConnection1.Params.Values['Server'] := '127.0.0.1';
  FDConnection1.Params.Values['Database'] := 'MyDatabase';
  FDConnection1.Params.Values['User_Name'] := 'sa';
  FDConnection1.Params.Values['Password'] := 'myPassword';
  try
    FDConnection1.Connected := True;
    FDQuery1.SQL.Text := 'SELECT * FROM MyTable';
    FDQuery1.Active := True;
    ShowMessage('Data loaded successfully!');
  except
    on E: Exception do
      ShowMessage('Error: ' + E.Message);
  end;
end;
```

---

### Alternatives to FireDAC
If you're using an older version of Delphi or cannot use FireDAC, consider:
1. **ADO (ActiveX Data Objects)**:
   - Use `TADOConnection`, `TADOQuery`, or `TADOTable` components.
   - Connection String example:
     ```
     Provider=SQLOLEDB;Data Source=127.0.0.1;Initial Catalog=MyDatabase;User ID=sa;Password=myPassword;
     ```

2. **Third-Party Libraries**: 
   - Libraries like dbExpress, UniDAC, or ZeosLib can also connect to SQL Server.
