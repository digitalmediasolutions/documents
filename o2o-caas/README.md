## UML diagrams

**ER-diagram**

```mermaid
erDiagram  
 ACCOUNTS  }|--|{  ACCOUNT-TEMPLATES: i 
 ACCOUNTS  {  
 string email  
 string type  
 string token 
 string variables 
 }  
  EMAIL-TEMPLATES  }|--|{  ACCOUNT-TEMPLATES  : i  
 EMAIL-TEMPLATES  {  
 string template
 string type
 object subject
 object content  
 array variables  
 }  
 ACCOUNT-TEMPLATES  {  
 string template
 string type
 object subject
 object content  
 array variables  
 }
  ```

