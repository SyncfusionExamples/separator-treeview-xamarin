# How to show the separator in Xamarin.Forms TreeView (SfTreeView)

You can add a separator for the whole row by customizing the [SfTreeView](https://help.syncfusion.com/xamarin/treeview/overview?) expander and indentation in Xamarin.Forms.

You can also refer the following article.

https://www.syncfusion.com/kb/11440/how-to-show-the-separator-in-xamarin-forms-treeview-sftreeview

**XAML**

Set [ExpanderWidth](https://help.syncfusion.com/xamarin/treeview/overview?) and [Indentation](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.SfTreeView.XForms~Syncfusion.XForms.TreeView.SfTreeView~Indentation.html?) to **zero** to disable the default expander and indentation. 
``` xml
<treeview:SfTreeView x:Name="treeView"
                    ItemHeight="40"
                    Indentation="0"
                    ExpanderWidth="0"
                    AutoExpandMode="None"
                    ItemTemplateContextType="Node"
                    ChildPropertyName="SubFiles"
                    ExpandActionTarget="Node"
                    ItemsSource="{Binding ImageNodeInfo}">
...
</treeview:SfTreeView>
```
Use the [converter](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/data-binding/converters) to display custom expander based on [IsExpanded](https://help.syncfusion.com/cr/xamarin/Syncfusion.SfTreeView.XForms~Syncfusion.TreeView.Engine.TreeViewNode~IsExpanded.html?) and indentation based on the [Level](https://help.syncfusion.com/cr/xamarin/Syncfusion.SfTreeView.XForms~Syncfusion.TreeView.Engine.TreeViewNode~Level.html?) property of TreeViewNode. Use the [BoxView](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/user-interface/boxview) with [HeightRequest](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.visualelement.heightrequest?view=xamarin-forms#Xamarin_Forms_VisualElement_HeightRequest) as 1 to display the separator line.
``` xml
<treeview:SfTreeView.ItemTemplate>
    <DataTemplate>
        <Grid x:Name="grid" Padding="5,5,5,5" RowSpacing="0" >
            <Grid.RowDefinitions>
                <RowDefinition Height="*"/>
                <RowDefinition Height="1"/>
            </Grid.RowDefinitions>
            <Grid>
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="{Binding Level, Converter={StaticResource IndentationConverter}}" />
                    <ColumnDefinition Width="35" />
                    <ColumnDefinition Width="35" />
                    <ColumnDefinition Width="*" />
                </Grid.ColumnDefinitions>
 
                <Image Grid.Column="1" Source="{Binding IsExpanded,Converter={StaticResource ExpanderIconConverter}}"
                        IsVisible="{Binding HasChildNodes,Converter={StaticResource ExpanderIconVisibilityConverter}}"
                            VerticalOptions="Center" 
                            HorizontalOptions="Center"
                            HeightRequest="15" 
                            WidthRequest="15"/>
                <Image Grid.Column="2" Source="{Binding Content.ImageIcon}" VerticalOptions="Center" HorizontalOptions="Start" HeightRequest="35" WidthRequest="35"/>
                <Grid Grid.Column="3" RowSpacing="1" Padding="1,0,0,0" VerticalOptions="Center">
                    <Label LineBreakMode="NoWrap" Text="{Binding Content.ItemName}" VerticalTextAlignment="Center"/>
                </Grid>
            </Grid>
            <BoxView HeightRequest="1" BackgroundColor="Gray" Grid.Row="1"/>
        </Grid>
    </DataTemplate>
</treeview:SfTreeView.ItemTemplate>
```
You can also refer to the following article to use the custom expander icon in Xamarin.Forms SfTreeView,
[CustomExpanderIcon](https://www.syncfusion.com/kb/10289/how-to-expand-and-collapse-treeview-node-using-image-instead-expander)

**C#**

Converter to return the indentation value based on the node level.
``` C#
public class IndentationConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        return (int)value * 40;
    }
 
    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        throw new NotImplementedException();
    }
}
```
**Output**

![TreeViewSeparator](https://github.com/SyncfusionExamples/separator-treeview-xamarin/blob/master/ScreenShots/TreeViewSeparator.jpg)
