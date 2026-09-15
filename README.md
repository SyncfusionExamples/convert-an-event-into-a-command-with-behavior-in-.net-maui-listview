# How to convert events into commands in .NET MAUI ListView (SfListView)?

The [.NET MAUI ListView](https://www.syncfusion.com/maui-controls/maui-listView) allows you to convert the events into commands using [Behaviors](https://learn.microsoft.com/en-us/dotnet/maui/fundamentals/behaviors?view=net-maui-8.0) to follow the MVVM pattern.

**C#**
To achieve this, need to create a command for the ItemTapped event of the SfListView in the ViewModel.
 
 ```
 public class ContactsViewModel : INotifyPropertyChanged
 {
     #region Properties

     public Command<Syncfusion.Maui.ListView.ItemTappedEventArgs> tapCommand;

     public Command<Syncfusion.Maui.ListView.ItemTappedEventArgs> TapCommand
     {
         get { return tapCommand; }
         set { tapCommand = value; OnPropertyChanged("TapCommand"); }
     }

     #endregion

     #region Constructor

     public ContactsViewModel()
     {
        TapCommand = new Command<Syncfusion.Maui.ListView.ItemTappedEventArgs>(OnTapCommand);
     }

     private void OnTapCommand(Syncfusion.Maui.ListView.ItemTappedEventArgs obj)
     {
         var name = (obj.DataItem as Contacts).ContactName;
         var number = (obj.DataItem as Contacts).ContactNumber;
         App.Current.MainPage.DisplayAlert(name, "Number:" + number, "Ok");
     }

 ```
 

**XAML**

 Associate the command to the appropriate event of SfListView using Behaviors, as shown below.
 ```
<syncfusion:SfListView x:Name="listView" >
  <syncfusion:SfListView.Behaviors>
    <local:EventToCommandBehavior EventName="ItemTapped"
                                  Command="{Binding TapCommand}">
    </local:EventToCommandBehavior>
  </syncfusion:SfListView.Behaviors>
</syncfusion:SfListView>
 ```
 
Now, when an item in the ListView is tapped, the corresponding Command in the ViewModel will be invoked automatically, performing the desired operation, as illustrated in the screenshot.


**Conclusion:**

I hope you enjoyed learning how to convert events into commands in .NET MAUI ListView (SfListView).

You can refer to our [.NET MAUI ListView](https://www.syncfusion.com/maui-controls/maui-listView) feature tour page to know about its other groundbreaking feature representations and [documentation](https://help.syncfusion.com/maui/listview/getting-started), and how to quickly get started with configuration specifications. 

Check out our components from the [License and Downloads](https://www.syncfusion.com/sales/teamlicense) page for current customers. If you are new to Syncfusion®, try our 30-day [free trial](https://www.syncfusion.com/downloads/maui) to check out our other controls.

Please let us know in the comments section if you have any queries or require clarification. You can also contact us through our [support forums](https://www.syncfusion.com/forums/), [Direct-Trac](https://support.syncfusion.com/create), or [feedback portal](https://www.syncfusion.com/feedback/maui?control=sflistview). We are always happy to assist you!
