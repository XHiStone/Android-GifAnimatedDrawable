# Android-GifAnimatedDrawable
Android-GifAnimatedDrawable加载Gif动态图片框架
##使用方法
下载dist文件夹中[sdk框架](https://github.com/18337129968/Android-GifAnimatedDrawable/tree/master/dist "gifanimatdedrawble框架SDK")，添加到项目lib中
##Activity中调用相关类实例化对象
```
//调用gifanimatdedrawble框架
public class DisplayGIF extends Activity implements OnClickListener 
{
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
	public boolean onCreateOptionsMenu(Menu menu) {
		// Inflate the menu; this adds items to the action bar if it is present.
		getMenuInflater().inflate(R.menu.display_gi, menu);
		return true;
	}

	@Override
	public void onClick(View arg0)
	{
		//((GifAnimationDrawable)imagebutton.getDrawable()).setVisible(true, true);
		((GifAnimationDrawable)imagebutton.getDrawable()).setVisible(true, true);
		if(imageview.getDrawable() == null) imageview.setImageDrawable(big);
		big.setVisible(true, true);
	}
}
