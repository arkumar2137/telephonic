# Questions List
1. [What are the types of Exceptions? Explain the hierarchy of Java Exception classes?](#q-what-are-the-types-of-exceptions-explain-the-hierarchy-of-java-exception-classes)

## Q. ***What are the types of Exceptions? Explain the hierarchy of Java Exception classes?***
Exception is an error event that can happen during the execution of a program and disrupts its normal flow.

**Types of Java Exceptions**  
**1. Checked Exception**: The classes which directly inherit `Throwable class` except RuntimeException and Error are known as checked exceptions e.g. IOException, SQLException etc. Checked exceptions are checked at compile-time.  
**2. Unchecked Exception**: The classes which inherit `RuntimeException` are known as unchecked exceptions e.g. ArithmeticException, NullPointerException, ArrayIndexOutOfBoundsException etc. Unchecked exceptions are not checked at compile-time, but they are checked at runtime.  
**3. Error**: Error is irrecoverable e.g. OutOfMemoryError, VirtualMachineError, AssertionError etc.

**Hierarchy of Java Exception classes**   
The java.lang.Throwable class is the root class of Java Exception hierarchy which is inherited by two subclasses: Exception and Error.

<img src="assets/exception-hierarchy-in-java.png" alt="Java Exception" />



Example:
```java
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.InputStream;

public class CustomExceptionExample {

	public static void main(String[] args) throws MyException {
		try {
			processFile("file.txt");
		} catch (MyException e) {
			processErrorCodes(e);
		}
	}

	private static void processErrorCodes(MyException e) throws MyException {
		switch(e.getErrorCode()){
		  case "BAD_FILE_TYPE":
			 System.out.println("Bad File Type, notify user");
			 throw e;
		  case "FILE_NOT_FOUND_EXCEPTION":
			 System.out.println("File Not Found, notify user");
			 throw e;
		  case "FILE_CLOSE_EXCEPTION":
			 System.out.println("File Close failed, just log it.");
			 break;
		  default:
			 System.out.println("Unknown exception occured," +e.getMessage());
			 e.printStackTrace();
		}
	}

	private static void processFile(String file) throws MyException {		
		InputStream fis = null;
		try {
			fis = new FileInputStream(file);
		} catch (FileNotFoundException e) {
			throw new MyException(e.getMessage(),"FILE_NOT_FOUND_EXCEPTION");
		} finally {
			try {
				if(fis !=null) fis.close();
			} catch (IOException e) {
				throw new MyException(e.getMessage(),"FILE_CLOSE_EXCEPTION");
			}
		}
	}
}
```
<div align="right">
    <b><a href="##questions-list">↥ back to top</a></b>
</div>