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
=
# ANT打包方法
-
##到官网下载[apache-ant-1.9.6](http://archive.apache.org/dist/ant/binaries/ "所有版本")解压并配置好环境变量
```
<?xml version="1.0"?>
<!-- 定义生成文件的project根元素，默认target为空，定义三个简单属性 -->
<project
    name="gifanimationdrawable"
    basedir="."
    default="package" >

    <!-- 设置系统的环境变量为前缀 env. -->
    <property environment="env" />
    
    <!-- 定义第三方jar包路径id为build.classpath -->
    <path id="build.classpath" >
        <!-- 编译过程会调用到安卓sdk第三方jar包 -->
        <fileset dir="E:\adt-bundle-windows-x86-20140321\sdk\platforms\android-20" >
            <include name="android.jar" />
        </fileset>
    </path>
    
    <!-- 定义初始化target文件目录集 -->
    <target name="init" >

        <property
            name="build"
            value="build" />

        <property
            name="dist"
            value="dist" />

        <property
            name="src"
            value="src" />
    </target>
	<!-- 定义清理target集 -->
    <target
        name="clean"
        depends="init" >

        <delete>

            <fileset
                casesensitive="no"
                defaultexcludes="no"
                dir="${src}" >

                <include name="**/*~" />

                <include name="**/*.class" />

                <exclude name="**/CVS" />

                <exclude name="**/CVS/**" />

                <exclude name="**/.cvsignore" />
            </fileset>

            <fileset
                dir="${build}"
                includes="**/*.class" />

            <fileset
                dir="${dist}"
                includes="${ant.project.name}.jar" />

            <fileset
                casesensitive="no"
                defaultexcludes="no"
                dir="." >

                <include name="**/*~" />
            </fileset>
        </delete>
    </target>
	<!-- 定义java编译target -->
    <target
        name="compile"
        depends="init" >
		<!-- 创建目录前删除目录 -->
        <delete dir="${build}" />

        <mkdir dir="${build}" />
		<!-- 编译java后的class放到build目录文件夹里 -->
        <javac
            debug="${debug}"
            deprecation="${deprecation}"
            destdir="${build}"
            <!--排除所列文件excludes固有属性  -->
            excludes="com/hipmob/gifanimationdrawable/sample/DisplayGIF.java"
            includeantruntime="false"
            optimize="${optimize}"
            source="1.5"
            target="1.5" >
			<!-- 指定所需要编译java文件所在位置 -->
            <src path="${src}" />
			<!-- 指定编辑java文件所需的第三方类库所在位置 -->
            <classpath refid="build.classpath" />
        </javac>
    </target>

    <target
        name="package"
        depends="compile" >
		<!-- 创建存放jar包目录前删除，以前目录 -->
        <delete dir="${dist}" />

        <mkdir dir="${dist}" />
		<!-- 把编译完成的class打包到dist（dest）文件目录下 -->
        <jar
            basedir="${build}"
            destfile="${dist}/${ant.project.name}.jar"
            includes="com/hipmob/gifanimationdrawable/*.class" >

            <!-- 打包过程不可使用文件集，includes=""是jar包固有属性为清单文件添加属性 -->
            <!--
            <fileset dir="${build}" >

                <include name="com/hipmob/gifanimationdrawable/*.class" />
            </fileset>



            -->
        </jar>
    </target>

</project>