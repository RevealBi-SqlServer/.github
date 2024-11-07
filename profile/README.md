## Hi there 👋

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->

### Developer's Guide to PoC Kickoff

*   **Dependencies:** The essential dependencies for a .NET Core application using Reveal are the Reveal NuGet package and the SQL Server dependency. The versions mentioned are 1.6.7 for Reveal, and 1.7.1 may be available. Other data sources like MySQL and Oracle can also be added.
*   **Integrating Reveal:** Reveal is integrated into the application through the program.cs file. After adding the NuGet packages, the following lines of code are used: `builder.Services.AddControllers().AddReveal()`. Then, interfaces like ObjectFilter and UserContextProvider are added as needed. Authentication and a data source provider are mandatory.
*   **Authentication:** Authentication is handled by implementing the `IRVAuthenticationProvider`. A username and password credential are created, and the connection details are stored in the data source provider. The example utilizes an Azure SQL instance.
*   **Data Source Provider:** The `DataSourceProvider` specifies the location of the database, including host, database name, schema, and port. This information can be retrieved from various sources, such as app settings, Azure Key Vault, or configuration files. The example uses app settings to store these details.
*   **HTML Client Setup:** The HTML client requires three dependencies: jQuery, JS, and the Reveal JavaScript library. These can be accessed locally or through a CDN. The client code specifies the server URL and a callback function that handles user interaction.
*   **Object Filter:** The `ObjectFilter` controls the data access permissions for users. It has a `Filter` function that can be customized to restrict data visibility based on user roles or other criteria. The example demonstrates a scenario where users with the "user" role can only access "All Orders" and "Invoices" data.
*   **User Context:** The `UserContext` provides information about the logged-in user. It can be used to store default properties like UserID or other custom properties defined in the `UserContextProvider`. The `GetUserContext` method is used to retrieve the user context.
*   **Additional Headers Provider:** The `SetAdditionalHeadersProvider` API allows passing custom headers to the server. These headers can contain information like customer ID or other relevant details.
*   **Data Source Items:** Custom data source items can be created, such as parameterized queries and stored procedures. These items are defined in the `DataSourceProvider` and are made accessible to users through a dialog.
*   **Dashboard Provider:** The `DashboardProvider` enables customization of dashboard saving behavior. It can be used to determine the save location based on the user's context, like saving to different folders or databases.
*   **Loading Dashboards:** Dashboards are loaded using the `LoadDashboard` function, which takes the name of the dashboard file as a parameter. In HTML clients, a selector is used to specify where the dashboard should be rendered.
*   **React Client Setup:** The React client follows a similar structure to the HTML client. It utilizes hooks and the Reveal JavaScript library. The base URL for the server needs to be set globally, either in a configuration file or within a globally loaded component like `app.module.ts` in Angular.
*   **Reveal SDK DOM:** The `Reveal.SDK.DOM` library, currently in beta, provides a typed view of dashboards. It allows easy access to dashboard properties, such as file name and title.
*   **Dashboard Titles vs. File Names:** The dashboard title displayed to the user can differ from the underlying file name. The `DashboardsThumbnail` and `DashboardsNames` APIs are used to retrieve both the title and file name, ensuring consistency in user experience.
*   **Licensing:** A trial license key is valid for 30 days and can be extended upon request. When a license is purchased, the key is valid for the duration of the contract. It's important to keep track of the license expiry date to avoid disruptions. The license key can be set in code, configuration files, or the home directory.
*   **Resources:** The following resources are available to help with the PoC:
    *   **Documentation:** Comprehensive documentation covering installation, licensing, and various features.
    *   **GitHub:** The Reveal BI GitHub repository contains SDK samples, issue tracking for bug reports and feature requests, and discussions for community support.
    *   **Discord Channel:** A Discord channel dedicated to Reveal provides direct interaction with the product team.
    *   **YouTube Channel:** Webinars and videos covering various aspects of Reveal are available on the YouTube channel.
    *   **JavaScript API:** Reveal offers a comprehensive JavaScript API that allows customization of almost every aspect of the dashboard, including visualization chooser, editing modes, and adding custom elements.

*   **Check-in Calls:** Weekly check-in calls lasting 10-15 minutes will be scheduled to provide updates and address any challenges during the PoC.
