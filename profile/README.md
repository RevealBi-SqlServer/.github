# Reveal Overview & Important Notes for a PoC Kickoff

## Dependencies

The essential dependencies for a .NET Core application using Reveal are the Reveal NuGet package and the SQL Server dependency.

## Integrating Reveal

Reveal is integrated into a .NET Core application through the `Program.cs` file. After adding the NuGet packages, dependency injection is configured to include Reveal services. Here’s the setup in `Program.cs`:

```csharp
builder.Services.AddControllers().AddReveal(builder =>
{
    builder
        .AddAuthenticationProvider<AuthenticationProvider>()
        .AddDataSourceProvider<DataSourceProvider>()
        .AddUserContextProvider<UserContextProvider>()
        .AddObjectFilter<ObjectFilterProvider>()
        .DataSources.RegisterMicrosoftSqlServer();
});
```

In this setup:
- **AddReveal Configuration**: Registers essential services like `AuthenticationProvider` and `DataSourceProvider`, while including optional configurations such as `UserContextProvider`, `ObjectFilterProvider`, and `DashboardProvider` as needed.
- **Data Sources**: Registers the Microsoft SQL Server connector, which is necessary for SQL Server integrations.

### Core Server Functions

#### Authentication

Authentication is handled by implementing the `IRVAuthenticationProvider`. A username and password credential are created, and the connection details are stored in the data source provider. The example utilizes an Azure SQL instance.

#### Data Source Provider

The `DataSourceProvider` specifies the location of the database, including host, database name, schema, and port. This information can be retrieved from various sources, such as app settings, Azure Key Vault, or configuration files. The example uses app settings to store these details.

#### Data Source Items

Custom data source items can be created, such as parameterized queries and stored procedures. These items are defined in the `DataSourceProvider` and are made accessible to users through a dialog.

### Optional, but Important Server Functions

#### Object Filter

The `ObjectFilter` controls the data access permissions for users. It has a `Filter` function that can be customized to restrict data visibility based on user roles or other criteria. The example demonstrates a scenario where users with the "user" role can only access "All Orders" and "Invoices" data.

#### User Context

The `UserContext` provides information about the logged-in user. It can be used to store default properties like `UserID` or other custom properties defined in the `UserContextProvider`. The `GetUserContext` method is used to retrieve the user context.

#### Dashboard Provider

The `DashboardProvider` enables customization of dashboard saving behavior. It can be used to determine the save location based on the user's context, like saving to different folders or databases.

## Setting up the Client

### HTML Client Setup

The HTML client requires three dependencies: jQuery, JS, and the Reveal JavaScript library. These can be accessed locally or through a CDN. The client code specifies the server URL and a callback function that handles user interaction.

### Loading Dashboards

Dashboards are loaded using the `LoadDashboard` function, which takes the name of the dashboard file as a parameter. In HTML clients, a selector is used to specify where the dashboard should be rendered.

### Additional Headers Provider

The `SetAdditionalHeadersProvider` API allows passing custom headers to the server. These headers can contain information like customer ID or other relevant details.

### Adding Custom Menu Items to Visualizations

In Reveal, you can customize the menu that appears on specific visualizations using the `onMenuOpening` event. This can be especially useful for adding custom actions directly accessible to users from visualizations.

When configuring a Reveal view, use the `onMenuOpening` handler to dynamically inject menu items based on conditions (such as specific visualization titles or user roles). This functionality is helpful for tailoring the user experience in interactive dashboards.

### Using the Reveal SDK DOM

The `Reveal.SDK.DOM` library, currently in beta, provides a typed view of dashboards. It allows easy access to dashboard properties, such as file name and title.

#### Dashboard Titles vs. File Names

The dashboard title displayed to the user can differ from the underlying file name. The `DashboardsThumbnail` and `DashboardsNames` APIs are used to retrieve both the title and file name, ensuring consistency in user experience.

## Licensing

A trial license key is valid for 30 days and can be extended upon request. When a license is purchased, the key is valid for the duration of the contract. It's important to keep track of the license expiry date to avoid disruptions. The license key can be set in code, configuration files, or the home directory.

## Resources

The following resources are available to help with the PoC:

- **[Documentation](https://help.revealbi.io/web/)**: Comprehensive documentation covering installation, licensing, and various features.
- **[GitHub](https://github.com/RevealBi/sdk-samples-javascript)**: The Reveal BI GitHub repository contains SDK samples, issue tracking for bug reports and feature requests, and discussions for community support.
- **Support via Discord Channel**: A Discord channel dedicated to Reveal provides direct interaction with the product team.
- **[Support via GitHub Discussions](https://github.com/RevealBi/Reveal.Sdk/discussions)**: A GitHub channel dedicated to Reveal provides direct interaction with the product team. Usually you'd use this if you can't access Discord due to corporate policy.
- **[YouTube Channel](https://www.youtube.com/@RevealBI/videos)**: Webinars and videos covering various aspects of Reveal are available on the YouTube channel.
- **[JavaScript API](https://help.revealbi.io/api/javascript/latest/)**: Reveal offers a comprehensive JavaScript API that allows customization of almost every aspect of the dashboard, including visualization chooser, editing modes, and adding custom elements.
- **[User Documentation](https://help.revealbi.io/user/)**: Detailed documentation for end users of Reveal.
- **[Developer Playground](https://help.revealbi.io/playground/)**: An interactive playground to experiment with Reveal BI's features.
- **[Add Feature Requests, Bug, Review Open Issues](https://github.com/RevealBi/Reveal.Sdk/issues)**: Reveal's GitHub repository where you can review, add, comment on new or existing issues.

## PoC Requirements

### Check-in Calls

Weekly check-in calls lasting 10-15 minutes will be scheduled to provide updates and address any challenges during the PoC.

--- 
