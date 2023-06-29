# Day 90

Date Completed: June 27, 2023 11:40 PM

Date Started: June 27, 2023 10:00 PM

Difficulty: ⭐⭐

Done: Yes

Languages: Android Development, Kotlin, XML

Related to Progress (Days): Your Progress 90%

Topic: Undo Functionality in Doodle It

## What I Learned Today

- Undo Functionality in Doodle It

## Key Concepts

## **Implement the "Undo" Feature**

### 1. Modify the activity_main.xml Layout File

Open the activity_main.xml layout file and add the following code snippet to include the "Undo" button:

```xml
<ImageButton
    android:id="@+id/undoButton"
    android:layout_width="50dp"
    android:layout_height="50dp"
    android:src="@drawable/undo_small_svgrepo_com" />
```

Explanation:

- We add an **`ImageButton`** with the ID **`undoButton`** to the layout. This button will serve as the "Undo" button for the user to go back to the previous step of drawing.
- Adjust the attributes (**`layout_width`**, **`layout_height`**, and **`src`**) based on your design requirements. The **`src`** attribute specifies the image resource for the button.

### 2. Modify the MainActivity.kt File

Inside the **`onCreate`** method of the MainActivity class, add the following code snippet to initialize the "Undo" button and set its click listener:

```kotlin
class MainActivity : AppCompatActivity() {
    private var drawingView: DrawingView? = null

    override fun onCreate(savedInstanceState: Bundle?) {
        // ...

        val ibUndo: ImageButton = findViewById(R.id.undoButton)
        ibUndo.setOnClickListener {
            drawingView?.onClickUndo()
        }
    }

    // ...
}
```

Explanation:

- We find the "Undo" button using its ID **`undoButton`** and assign it to the **`ibUndo`** variable.
- We set a click listener on the button that calls the **`onClickUndo`** function in the **`DrawingView`** class.

### 3 Modify the DrawingView.kt File

Inside the DrawingView class, add the following function to handle the "Undo" functionality:

```kotlin
class DrawingView(context: Context, attrs: AttributeSet) : View(context, attrs) {
    // ...

    fun onClickUndo() {
        if (mPaths.size > 0) {
            mUndoPaths.add(mPaths.removeAt(mPaths.size - 1))
            invalidate()
        }
    }

    // ...
}
```

Explanation:

- The **`onClickUndo`** function is called when the "Undo" button is clicked.
- If there are paths stored in the **`mPaths`** ArrayList, the last path is removed from **`mPaths`** and added to the **`mUndoPaths`** ArrayList. The **`invalidate`** function is then called to refresh the drawing view.

### 4. Update the onDraw Function

Inside the **`onDraw`** function of the DrawingView class, add the following code snippet to handle the drawing of paths and the "Undo" action:

```kotlin
class DrawingView(context: Context, attrs: AttributeSet) : View(context, attrs) {
    // ...

    override fun onDraw(canvas: Canvas) {
        super.onDraw(canvas)

        // Draw the canvas bitmap
        canvas.drawBitmap(mCanvasBitmap!!, 0f, 0f, mCanvasPaint)

        // Draw the stored paths
        for (path in mPaths) {
            mDrawPaint!!.strokeWidth = path.brushThickness
            mDrawPaint!!.color = path.color
            canvas.drawPath(path, mDrawPaint!!)
        }

        // Draw the current path being drawn
        if (!mDrawPath!!.isEmpty) {
            mDrawPaint!!.strokeWidth = mDrawPath!!.brushThickness
            mDrawPaint!!.color = mDrawPath!!.color
            canvas.drawPath(mDrawPath!!, mDrawPaint!!)
        }
    }

    // ...
}
```

Explanation:

- Inside the **`onDraw`** function, we first draw the canvas bitmap using the **`drawBitmap`** function.
- Then, we iterate through the stored paths in **`mPaths`** and draw them on the canvas using the appropriate brush thickness and color.
- Finally, we draw the current path (**`mDrawPath`**) being drawn on top of the stored paths.

### 5. Update the onTouchEvent Function

Inside the **`onTouchEvent`** function of the DrawingView class, update the **`MotionEvent.ACTION_UP`** case as follows:

```kotlin
class DrawingView(context: Context, attrs: AttributeSet) : View(context, attrs) {
    // ...

    override fun onTouchEvent(event: MotionEvent?): Boolean {
        // ...

        when (event?.action) {
            // ...

            MotionEvent.ACTION_UP -> {
                mPaths.add(mDrawPath!!)
                mDrawPath = CustomPath(color, mBrushSize)
            }

            // ...
        }
        invalidate()
        return true
    }

    // ...
}
```

Explanation:

- When the user releases the touch (**`MotionEvent.ACTION_UP`**), we add the current path (**`mDrawPath`**) to the **`mPaths`** ArrayList. Then, we create a new instance of **`CustomPath`** and assign it to **`mDrawPath`** for the next drawing operation.

### **Conclusion**

By following the steps outlined in this documentation, you have successfully implemented the "Undo" feature in the "Doodle It" Android application. Users can now undo their drawings by clicking the "Undo" button, allowing them to go back to the previous step of drawing.

Please note that the provided code snippets assume that the necessary import statements and other required components are in place. Additionally, ensure that the layout file (**`activity_main.xml`**) contains all the necessary views and attributes based on the provided code.

Remember to test the application thoroughly and handle any potential exceptions or edge cases that may arise when using the "Undo" functionality.

## Challenges Experienced

Nothing at all.

## Resources Used

Udemy, Udacity, ChatGPT, Documentation
