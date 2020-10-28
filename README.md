# Android_Kotlin_developer_nanodegree

#### Data Binding:


- Data Binding - The Idea
The big idea about data binding is to create an object that connects/maps/binds two pieces of distant information together at compile time, so that you don't have to look for it at runtime.
The object that surfaces these bindings to you is called the Binding object. It is created by the compiler, and while understanding how it works under the hood is interesting, it is not necessary to know for basic uses of data binding.

- Data Binding and findViewById
findViewById is a costly operation because it traverses the view hierarchy every time it is called.
With data binding enabled, the compiler creates references to all views in a <layout> that have an id, and gathers them in a Binding object.
In your code, you create an instance of the binding object, and then reference views through the binding object with no extra overhead.
  


- In Activity:
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)

    val binding: ActivityMainBinding = DataBindingUtil.setContentView(
            this, R.layout.activity_main)

    binding.user = User("Test", "User")
}

Alternatively we can use
val binding: ActivityMainBinding = ActivityMainBinding.inflate(getLayoutInflater())


- In Fragment:

If you are using data binding items inside a Fragment, ListView, or RecyclerView adapter, you may prefer to use the inflate() methods of the bindings classes or the DataBindingUtil class, as shown in the following code example:

val listItemBinding = ListItemBinding.inflate(layoutInflater, viewGroup, false)
// or
val listItemBinding = DataBindingUtil.inflate(layoutInflater, R.layout.list_item, viewGroup, false)


- In your build.gradle file in the app module, enable data binding inside the android section:

buildFeatures {
      dataBinding true
}
Wrap all views in activity_main.xml into a <layout> tag, and move the namespace declarations into the the <layout> tag.

* In MainActivity, create a binding object:
private lateinit var binding: ActivityMainBinding

* In onCreate, use DataBindingUtil to set the content view:
binding = DataBindingUtil.setContentView(this, R.layout.activity_main)
*
Use the binding object to replace all calls to findViewById, for example:
binding.doneButton.setOnClickListener….etc
Hint: You can use apply() in the click handler to make your code more concise and readable.

* Create a data class MyName for the name and nickname.
data class MyName(var name: String = "", var nickname: String = "")
Add a <data> block to activity_main.xml. The data block goes inside the layout tag but before the view tags. Inside the data block, add a variable for the MyName class.
<data>
<!-- Declare a variable by specifying a name and a data type. -->
<!-- Use fully qualified name for the type. -->
<variable
    name="myName"
    type="com.example.android.aboutme.MyName" />
</data>
In name_text, nickname_edit, and nickname_text, replace the references to string text resources with references to the variables, for example>
android:text="@={myName.name}"
In MainActivity, create an instance of MyName.
// Instance of MyName data class.
private val myName: MyName = MyName("Aleks Haecky")
And in onCreate(), set binding.myName to it.
binding.myName = myName
In addNickname, set the value of nickname in myName, call invalidateAll(), and the data should show in your views.
myName?.nickname = nicknameEdit.text.toString()
// Invalidate all binding expressions and request a new rebind to refresh UI
invalidateAll()



### ViewModel


To initialize viewModel Fragment use this<br>
 viewModel = ViewModelProvider(this.activity!!).get(ShoeViewModel::class.java)
 * this.getAcitvity() argumentin ViewModelProvider is important. 
















