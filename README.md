# Android-GifAnimatedDrawable
Android-GifAnimatedDrawable加载Gif动态图片框架
gifanimatdedrawble框架已编译请到dist目录下载
使用方法：

        <ImageButton
        android:id="@+id/imagebutton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentLeft="true"
        android:layout_alignParentTop="true"
        android:layout_marginLeft="15dp"
        android:layout_marginTop="16dp" />
        <ImageView
        android:id="@+id/imageview"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/imagebutton"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="98dp" />
    
主程序：

	private ImageView imageview;
	private ImageButton imagebutton;
	private GifAnimationDrawable little, big;
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_display_gif);
		
		imageview = (ImageView)findViewById(R.id.imageview);
		imagebutton = (ImageButton)findViewById(R.id.imagebutton);
		
		imagebutton.setOnClickListener(this);
		
		// and add the GifAnimationDrawable
		try{
			android.util.Log.v("GifAnimationDrawable", "===>One");
			little = new GifAnimationDrawable(getResources().openRawResource(R.raw.anim1));
			little.setOneShot(true);
			android.util.Log.v("GifAnimationDrawable", "===>Two");
			imagebutton.setImageDrawable(little);
			android.util.Log.v("GifAnimationDrawable", "===>Three");
			big = new GifAnimationDrawable(getResources().openRawResource(R.raw.anim2));
			big.setOneShot(true);
			android.util.Log.v("GifAnimationDrawable", "===>Four");
		}catch(IOException ioe){
			
		}
	}

	@Override
	public void onClick(View arg0)
	{
		//((GifAnimationDrawable)imagebutton.getDrawable()).setVisible(true, true);
		((GifAnimationDrawable)imagebutton.getDrawable()).setVisible(true, true);
		if(imageview.getDrawable() == null) imageview.setImageDrawable(big);
		big.setVisible(true, true);
	}
