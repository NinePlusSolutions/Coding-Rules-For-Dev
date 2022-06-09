# Coding-Rules-For-Dev
Apply this rule for all dev in our office

##Coding Conventions

####1\. Project guidelines

**1.1 Project structure**

**1.2 File naming**

**1.2.1 Class files**

Class names are written in [UpperCamelCase](http://en.wikipedia.org/wiki/CamelCase).

For classes that extend an Android component, the name of the class should end with the name of the component; for example: SignInActivity, SignInFragment, ImageUploaderService, ChangePasswordDialog.

**1.2.2 Resources files**

Resources file names are written in **lowercase_underscore**.

**1.2.2.1 Drawable files**

Naming conventions for drawables:

| Asset Type   | Prefix            |		Example               |
|--------------| ------------------|-----------------------------|
| Action bar   | `ab_`             | `ab_stacked.9.png`          |
| Button       | `btn_`	            | `btn_send_pressed.9.png`    |
| Dialog       | `dialog_`         | `dialog_top.9.png`          |
| Divider      | `divider_`        | `divider_horizontal.9.png`  |
| Icon         | `ic_`	            | `ic_star.png`               |
| Menu         | `menu_	`           | `menu_submenu_bg.9.png`     |
| Notification | `notification_`	| `notification_bg.9.png`     |
| Tabs         | `tab_`            | `tab_pressed.9.png`         |

Naming conventions for icons

| Asset Type                      | Prefix             | Example                      |
| --------------------------------| ----------------   | ---------------------------- |
| Icons                           | `ic_`              | `ic_star.png`                |
| Launcher icons                  | `ic_launcher`      | `ic_launcher_calendar.png`   |
| Menu icons and Action Bar icons | `ic_menu`          | `ic_menu_archive.png`        |
| Status bar icons                | `ic_stat_notify`   | `ic_stat_notify_msg.png`     |
| Tab icons                       | `ic_tab`           | `ic_tab_recent.png`          |
| Dialog icons                    | `ic_dialog`        | `ic_dialog_info.png`         |

Naming conventions for selector states:

| State	       | Suffix          | Example                     |
|--------------|-----------------|-----------------------------|
| Normal       | `_normal`       | `btn_order_normal.9.png`    |
| Pressed      | `_pressed`      | `btn_order_pressed.9.png`   |
| Focused      | `_focused`      | `btn_order_focused.9.png`   |
| Disabled     | `_disabled`     | `btn_order_disabled.9.png`  |
| Selected     | `_selected`     | `btn_order_selected.9.png`  |

**1.2.2.2 Layout files**

Layout files should match the name of the Android components that they are intended for but moving the top level component name to the beginning. For example, if we are creating a layout for the SignInActivity, the name of the layout file should be activity_sign_in.xml.

| Component        | Class Name             | Layout Name                   |
| ---------------- | ---------------------- | ----------------------------- |
| Activity         | `UserProfileActivity`  | `activity_user_profile.xml`   |
| Fragment         | `SignUpFragment`       | `fragment_sign_up.xml`        |
| Dialog           | `ChangePasswordDialog` | `dialog_change_password.xml`  |
| AdapterView item | ---                    | `item_person.xml`             |
| Partial layout   | ---                    | `partial_stats_bar.xml`       |

A slightly different case is when we are creating a layout that is going to be inflated by an Adapter, e.g to populate a ListView. In this case, the name of the layout should start with item_.

Note that there are cases where these rules will not be possible to apply. For example, when creating layout files that are intended to be part of other layouts. In this case you should use the prefix partial_.

**1.2.2.3 Menu files**

Similar to layout files, menu files should match the name of the component. For example, if we are defining a menu file that is going to be used in the UserActivity, then the name of the file should be activity_user.xml

A good practice is to not include the word menu as part of the name because these files are already located in the menu directory.

**1.2.2.4 Values files**
Resource files in the values folder should be **plural**, e.g. strings.xml, styles.xml, colors.xml, dimens.xml, attrs.xml

####2 Code guidelines

**2.1 Java language rules**

**2.1.1 Don't ignore exceptions**

You must never do the following:

```Kotlin
fun setServerPort(value: String) {
    try {
        val serverPort = Integer.parseInt(value)
    } catch (e: NumberFormatException) { }
}
```

While you may think that your code will never encounter this error condition or that it is not important to handle it, ignoring exceptions like above creates mines in your code for someone else to trip over some day. You must handle every Exception in your code in some principled way. The specific handling varies depending on the case. - ([Android code style guidelines](https://source.android.com/source/code-style.html))

See alternatives [here](https://source.android.com/source/code-style.html#dont-ignore-exceptions).

**2.1.2 Don't catch generic exception**

You should not do this:
```kotlin
try {
    someComplicatedIOFunction() // may throw IOException
    someComplicatedParsingFunction()  // may throw ParsingException
    someComplicatedSecurityFunction() // may throw SecurityException
    // phew, made it all the way
} catch (e: Exception) {// I'll just catch all exceptions
    handleError() // with one generic handler!
}
```
See the reason why and some alternatives [here](https://source.android.com/source/code-style.html#dont-catch-generic-exception)

**2.1.3 Don't use finalizers**

We don't use finalizers. There are no guarantees as to when a finalizer will be called, or even that it will be called at all. In most cases, you can do what you need from a finalizer with good exception handling. If you absolutely need it, define a close() method and document exactly when that method needs to be called. See InputStream for an example. In this case it is appropriate but not required to print a short log message from the finalizer, as long as it is not expected to flood the logs. - ([Android code style guidelines](https://source.android.com/source/code-style.html#dont-use-finalizers))

**2.1.4 Fully qualify imports**

This is bad: `import foo.*`

This is good: `import foo.Bar`

See more info [here](https://source.android.com/source/code-style.html#fully-qualify-imports)

**2.2 Kotlin style rules**

**2.2.1 Treat acronyms as words**

| Good           | Bad            |
| -------------- | -------------- |
| `XmlHttpRequest` | `XMLHTTPRequest` |
| `getCustomerId`  | `getCustomerID`  |
| `String url`     | `String URL`     |
| `long id`        | `long ID`        |

**2.2.2 Use spaces for indentation**

Use **4 space** indents for blocks:
```kotlin
if (x ==  1) {
    x++
}
```
Use **8 space** indents for line wraps:
```kotlin
val i =
    someLongExpression(that, wouldNotFit, on, one, line);
```
**2.2.3 Annotations style**

**Classes, Methods and Constructors**

When annotations are applied to a class, method, or constructor, they are listed after the documentation block and should appear as **one annotation per line** .
```kotlin
/* This is the documentation block about the class */
@AnnotationA
@AnnotationB
class  MyAnnotatedClass { }
```
**Fields**

Annotations applying to fields should be listed **on the same line**, unless the line reaches the maximum line length.
```kotlin
@Nullable  @Mock mDataManager: DataManager;
```
**2.2.4 Class member ordering**

There is no single correct solution for this but using a **logical** and **consistent** order will improve code learnability and readability. It is recommendable to use the following order:

1.  Constants
2.  Fields
3.  Constructors
4.  Override methods and callbacks (public or private)
5.  Public methods
6.  Private methods
7.  Inner classes or interfaces

Example:
```kotlin
class  MainActivity: Activity() {

    private  val  TAG: String = MainActivity.class.getSimpleName()

    private var mTitle: String
    private var mTextViewTitle: TextView

    override  fun  onCreate() {
        ...
    }

    fun  setTitle(title: String) {
        mTitle = title
    }

    private  fun  setUpView() {
        ...
    }
}
```
If your class is extending an **Android component** such as an Activity or a Fragment, it is a good practice to order the override methods so that they **match the component's lifecycle**. For example, if you have an Activity that implements onCreate(), onDestroy(), onPause() and onResume(), then the correct order is:
```kotlin
class  MainActivity: Activity() {

//Order matches Activity lifecycle
 override fun  onCreate() {}

 override fun  onResume() {}

 override fun  onPause() {}

 override fun  onDestroy() {}
}
```
**2.2.5 Parameter ordering in methods**

When programming for Android, it is quite common to define methods that take a Context. If you are writing a method like this, then the **Context** must be the **first** parameter.

The opposite case are **callback** interfaces that should always be the **last** parameter.

Examples:
```kotlin
// Context always goes first
fun loadUser(context: Context, userId: Int): User

// Callbacks always go last
fun loadUserAsync(context: Context, userId: Int, callback: UserCallback)
```
**2.2.6 String constants, naming, and values**

Many elements of the Android SDK such as SharedPreferences, Bundle, or Intent use a key-value pair approach so it's very likely that even for a small app you end up having to write a lot of String constants.

When using one of these components, you **must** define the keys as a const val fields and they should be prefixed as indicated below.

| Element            | Field Name Prefix |
| -----------------  | ----------------- |
| SharedPreferences  | `PREF_`             |
| Bundle             | `BUNDLE_`           |
| Fragment Arguments | `ARGUMENT_`         |
| Intent Extra       | `EXTRA_`            |
| Intent Action      | `ACTION_`           |

Note that the arguments of a Fragment - Fragment.getArguments() - are also a Bundle. However, because this is a quite common use of Bundles, we define a different prefix for them.

Example:
```kotlin
// Note the value of the field is the same as the name to avoid duplication issues
const val PREF_EMAIL  =  "PREF_EMAIL"
const val BUNDLE_AGE  =  "BUNDLE_AGE"
const val ARGUMENT_USER_ID  =  "ARGUMENT_USER_ID"

// Intent-related items use full package name as value
const val EXTRA_SURNAME  =  "com.myapp.extras.EXTRA_SURNAME"
const val ACTION_OPEN_USER  =  "com.myapp.action.ACTION_OPEN_USER"
```
**2.2.7 Line length limit**

Code lines should not exceed **100 characters**. If the line is longer than this limit there are usually two options to reduce its length:

-   Extract a local variable or method (preferable).
-   Apply line-wrapping to divide a single line into multiple ones.

There are two **exceptions** where it is possible to have lines longer than 100:

-   Lines that are not possible to split, e.g. long URLs in comments.
-   package and import statements.

**2.2.7.1 Line-wrapping strategies**

There isn't an exact formula that explains how to line-wrap and quite often different solutions are valid. However there are a few rules that can be applied to common cases.

**Break at operators**

When the line is broken at an operator, the break comes **before** the operator. For example:

val longName = anotherVeryLongVariable + anEvenLongerOne- thisRidiculousLongOne

 + theFinalOne

**Assignment Operator Exception**

An exception to the break at operators rule is the assignment operator =, where the line break should happen **after** the operator.
```kotlin
val longName =
              anotherVeryLongVariable + anEvenLongerOne
              - thisRidiculousLongOne + theFinalOne
```
**Method chain case**

When multiple methods are chained in the same line - for example when using Builders - every call to a method should go in its own line, breaking the line before the .
```kotlin
Picasso.with(context)
    .load("http://ribot.co.uk/images/sexyjoe.jpg")
    .into(imageView)
```
**Long parameters case**

When a method has many parameters or its parameters are very long, we should break the line after every comma ,
```kotlin
loadPicture(context,
    "http://ribot.co.uk/images/sexyjoe.jpg",
    mImageViewProfilePicture,
    clickListener,
    "Title of the picture")
```
**2.3 XML style rules**

**2.3.1 Use self closing tags**

When an XML element doesn't have any contents, you **must** use self closing tags.

This is good:
```xml
<TextView
    android:id="@+id/tv_profile"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />
```
This is **bad** :
```xml
<!-- Don\'t do this! -->
<TextView
    android:id="@+id/tv_profile"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" >
</TextView>
```
**2.3.2 Resources naming**

Resource IDs and names are written in **lowercase_underscore**.

**2.3.2.1 ID naming**

IDs should be prefixed with the name of the element in lowercase underscore. For example:

| Element              | Prefix            |
| -----------------    | ----------------- |
| `TextView`           | `tv_`             |
| `ImageView`          | `iv_`             |
| `Button`             | `btn_`            |
| `Menu`               | `menu_`           |
| `EditText`           | `edt`             |
| `ProgressBar`        | `pb_`             |
| `Checkbox`           | `chk_`            |
| `Toolbar`            | `tb_`             |
| `RadioButton`        | `rb_`             |
| `Spinner`            | `spn_`            |
| `GalleryView`        | `gv_`             |
| `LinearLayout`       | `ll_`             |
| `RelativeLayout`     | `rl_`             |
| `RecyclerView`       | `rv_`             |
| `CoordinatorLayout`  | `cdl_`            |

Image view example:
```xml
<ImageView
    android:id="@+id/iv_profile"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />
```
Menu example:
```xml
<menu>
    <item
        android:id="@+id/menu_done"
        android:title="Done" />
</menu>
```
**2.3.2.2 Strings**

String names start with a prefix that identifies the section they belong to. For example registration_email_hint or registration_name_hint. If a string **doesn't belong** to any section, then you should follow the rules below:

| Prefix             | Description                           |
| -----------------  | --------------------------------------|
| `error_`             | An error message                      |
| `msg_`               | A regular information message         |
| `title_`             | A title, i.e. a dialog title          |
| `action_`            | An action such as "Save" or "Create"  |

**2.3.2.3 Styles and Themes**

Unlike the rest of resources, style names are written in **UpperCamelCase**.

**2.3.3 Attributes ordering**

As a general rule you should try to group similar attributes together. A good way of ordering the most common attributes is:

1.  View Id
2.  Style
3.  Layout width and layout height
4.  Other layout attributes, sorted alphabetically
5.  Remaining attributes, sorted alphabetically

# 3 Workflows

**3.1 Declare - branch name rules**

- Branch name must be cleared
- Easy to get meaning
- After branch has been merged > it must be deleted!

Example: update_user_profile

| BAD             | GOOD                           |
| -----------------  | --------------------------------------|
| fix_common             | fix_crash_when_login  |

**3.2 Rebase - Single commits**

- Always create PR and send to reviewer
- ONLY 1 commit in 1 PR
- Less than 10 files changed in 1 commit


**3.3 NO HARD CODE - NO DEAD CODE**

- No hard string > define constants or common function
- If code didn't use anymore, please delete

**3.4 Code commits**

EVERY COMMIT must be followed this rule: 

[action](scope function): [message detail].

- action: should be in: [build, ci, chore, docs, feat, fix, perf, refactor, revert, style, test, update]
- scope function: should be task/function implement
- message detail: clear message about your task or what you did on this commit

Example: update(Login): #ID_TASK - Changed login logics

| Prefix             | Example                           |
| -----------------  | --------------------------------------|
| `build`             | build(Login): #ID_TASK - Build login screen  |
| `ci`               | ci(Login): #ID_TASK - <message>  |
| `docs`             | docs(Login): #ID_TASK - <message>  |
| `feat`            | feat(Login): #ID_TASK - <message>  |
| `fix`            | fix(Login): #ID_TASK - <message>  |
| `perf`            | perf(Login): #ID_TASK - <message>  |
| `refactor`            | refactor(Login): #ID_TASK - <message>  |
| `revert`            | revert(Login): #ID_TASK - <message>  |
| `style`            | style(Login): #ID_TASK - <message>  |
| `test`            | test(Login): #ID_TASK - <message>  |
| `update`            | update(Login): #ID_TASK - <message>  |

