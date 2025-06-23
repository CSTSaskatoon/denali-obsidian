# Code Examples
- [Cheat Sheet](CST_Year2_S2/COSC-295-T01%20Advanced%20Mobile%20Application%20Programming/Final/Cheat%20Sheet.md#Table%20Of%20Contents)
## Layouts
- [Cheat Sheet](CST_Year2_S2/COSC-295-T01%20Advanced%20Mobile%20Application%20Programming/Final/Cheat%20Sheet.md#Table%20Of%20Contents)

## Navigation
- [Cheat Sheet](CST_Year2_S2/COSC-295-T01%20Advanced%20Mobile%20Application%20Programming/Final/Cheat%20Sheet.md#Table%20Of%20Contents)

### Basic Navigation Example
```cs
// App.xaml.cs
public App()
{
    InitializeComponent();

    MainPage = new NavigationPage(new MainPage());

    // Toolbar items
    ToolbarItem tb = new ToolbarItem
    {
        Text = "Go to root you fucking imbecile"
    };
    tb.Clicked += (sender, e) =>
    {
        MainPage.Navigation.PopToRootAsync();
    };
    MainPage.ToolbarItems.Add(tb);
}

// MainPage.xaml.cs
public partial class MainPage : ContentPage
{
	public MainPage()
	{
		InitializeComponent();
		btnNew.Clicked += (sender, e) =>
		{
			Navigation.PushAsync(new OurPage());
		};

		btnNewModal.Clicked += (sender, e) =>
		{
			Navigation.PushModalAsync(new OurPage());
		};
	}
}

// OurPage.xaml.cs
public partial class OurPage : ContentPage
{
    private static int count = 1;
    public OurPage()
    {
        InitializeComponent();

		btnNew.Clicked += (sender, e) =>
		{
			Navigation.PushAsync(new OurPage());
		};
		btnNewModal.Clicked += (sender, e) =>
		{
			Navigation.PushModalAsync(new OurPage());
		};
		btnClose.Clicked += (sender, e) =>
		{
			Navigation.PopAsync();
		};
		btnCloseModal.Clicked += (sender, e) =>
		{
			Navigation.PopModalAsync();
		};
		btnRoot.Clicked += (sender, e) =>
		{
			Navigation.PopToRootAsync();
		};

		Title = $"Fuckass navigation menu - {count++}";
	}
}
```

## List Views
- [Cheat Sheet](CST_Year2_S2/COSC-295-T01%20Advanced%20Mobile%20Application%20Programming/Final/Cheat%20Sheet.md#Table%20Of%20Contents)

## Sliders
- [Cheat Sheet](CST_Year2_S2/COSC-295-T01%20Advanced%20Mobile%20Application%20Programming/Final/Cheat%20Sheet.md#Table%20Of%20Contents)

### Rotating Text Example
```cs
//font slider
Slider slider = new Slider
{
    Minimum = 0,
    Maximum = 3,
    Value = currentFontSize == 12 ? 0 : currentFontSize == 16 ? 1 : currentFontSize == 18 ? 2 : 3,
    HorizontalOptions = LayoutOptions.FillAndExpand,
    ThumbColor = Color.DodgerBlue,
    MinimumTrackColor = Color.LightBlue,
};

// save on value change. 
slider.ValueChanged += (s, e) =>
{
    // Convert slider value to font size options
    int[] fontSizes = { 12, 16, 18, 24 };
    int fontIndex = (int)Math.Round(e.NewValue);
    int selectedFontSize = fontSizes[fontIndex];

    // Save to SecureStorage
    try
    {
        SecureStorage.SetAsync("FontPref", selectedFontSize.ToString()).GetAwaiter().GetResult();
    }
    catch (Exception ex)
    {
        App.Toast.Show("Failed to save font preference");
    }
};
```

## Persistent Storage
- [Cheat Sheet](CST_Year2_S2/COSC-295-T01%20Advanced%20Mobile%20Application%20Programming/Final/Cheat%20Sheet.md#Table%20Of%20Contents)

### Database SQL Query Example
```cs
db.Execute("SELECT * FROM Match WHERE ID = ?", id); db.Table<Match>().Where(i => i.ID == id).FirstOrDefault();
```

## BindingContext
- [Cheat Sheet](CST_Year2_S2/COSC-295-T01%20Advanced%20Mobile%20Application%20Programming/Final/Cheat%20Sheet.md#Table%20Of%20Contents)

### OnBindingContextChanged
```cs
/**
* Used to determine the count of matches for a game
*/
protected override void OnBindingContextChanged()
{
    base.OnBindingContextChanged();
   
	if (BindingContext is Game game)
	{
        matchCountLabel.Text = App.DB.GetMatchesByGame(game.ID).Count.ToString();
    }
    else 
    {
        matchCountLabel.Text = "0";
    }
}
```