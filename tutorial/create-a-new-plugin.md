# 2.1 Create Backend API

Before we start creating our app, we first need to create an API connected to a database. For this purpose, we will use a free tool called [Supabase](https://supabase.io).

### Step 1: Sign up

Go to [supabase.com](https://supabase.com) and Sign up to create a new account.

![](<../.gitbook/assets/supabase homepage (1).png>)

### **Step 2: Create a New Project**

Next, we need to create a new project. Click the "New Project" button once you login into the Supabase app, and follow the wizard to create your API project.

![2a. Click "New Project"](<../.gitbook/assets/Screenshot 2022-04-21 at 11.13.00 PM.png>) ![2b. Enter Organization Name](<../.gitbook/assets/Screenshot 2022-04-21 at 11.13.22 PM.png>) ![2c. Enter project details](<../.gitbook/assets/Screenshot 2022-04-21 at 11.14.01 PM.png>) ![2d. Project dashboard](<../.gitbook/assets/Screenshot 2022-04-21 at 11.14.31 PM.png>)

### **3. Create Database Table**

Now we need to create our database table to store our to-do tasks.

Start by clicking the Table Editor button on the left sidebar menu. Once you're on this page, press the "Create a new table" button.

![Press the "Create a new table" button](<../.gitbook/assets/Screenshot 2022-04-21 at 11.24.47 PM.png>)

When the form opens, add the following columns to match the screenshot below:

1. id (uuid)
2. title (varchar)
3. description (text)
4. completed (bool)
5. created\_at (timestamptz)

![Add table columns](<../.gitbook/assets/Screenshot 2022-04-21 at 11.27.30 PM.png>)

### **4. Build GraphQL Schema**

Since we are going to be building our app on top of [GraphQL](https://graphql.org) query language, we need to tell Supabase to build its schema.

On the left sidebar menu click the "SQL Editor" button. Once on this screen, press the "+ New Query" button.&#x20;

![](<../.gitbook/assets/Screenshot 2022-04-21 at 11.33.47 PM.png>)

Now enter the following code snippet in the editor and press "RUN"

```sql
-- Rebuild the GraphQL Schema Cache
select graphql.rebuild_schema();
```

![](<../.gitbook/assets/Screenshot 2022-04-21 at 11.40.13 PM.png>)

That's all. We're done with creating our API for the project. All we need to do is consume it now.
