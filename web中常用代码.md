package cn.itheima.response;

import java.awt.Color;
import java.awt.Font;
import java.awt.Graphics2D;
import java.awt.image.BufferedImage;
import java.io.IOException;
import java.util.Random;

import javax.imageio.ImageIO;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.swing.ImageIcon;
/**
 * 使用验证码的操作
 * @author asus
 *
 */
public class CodeServlet extends HttpServlet {

	/**
	 * 1、生成图片
	 * 2、生成随机的数字和字母
	 * 3、把数字和字母画到图片上
	 * 4、把图片显示在页面上
	 */
	public void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		int width = 150;
		int height = 50;
		//生成图片
		BufferedImage bufferedImage = new BufferedImage(width, height, BufferedImage.TYPE_3BYTE_BGR);
		//得到画笔
		Graphics2D g2d = (Graphics2D) bufferedImage.getGraphics();
		//生成四个随机的数字和字母
//		String words = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz1234567890";
		
		String words = "\u7684\u4e00\u4e86\u662f\u6211\u4e0d\u5728\u4eba\u4eec\u6709\u6765\u4ed6\u8fd9\u4e0a\u7740\u4e2a\u5730\u5230\u5927\u91cc\u8bf4\u5c31\u53bb\u5b50\u5f97\u4e5f\u548c\u90a3\u8981\u4e0b\u770b\u5929\u65f6\u8fc7\u51fa\u5c0f\u4e48\u8d77\u4f60\u90fd\u628a\u597d\u8fd8\u591a\u6ca1\u4e3a\u53c8\u53ef\u5bb6\u5b66\u53ea\u4ee5\u4e3b\u4f1a\u6837\u5e74\u60f3\u751f\u540c\u8001\u4e2d\u5341\u4ece\u81ea\u9762\u524d\u5934\u9053\u5b83\u540e\u7136\u8d70\u5f88\u50cf\u89c1\u4e24\u7528\u5979\u56fd\u52a8\u8fdb\u6210\u56de\u4ec0\u8fb9\u4f5c\u5bf9\u5f00\u800c\u5df1\u4e9b\u73b0\u5c71\u6c11\u5019\u7ecf\u53d1\u5de5\u5411\u4e8b\u547d\u7ed9\u957f\u6c34\u51e0\u4e49\u4e09\u58f0\u4e8e\u9ad8\u624b\u77e5\u7406\u773c\u5fd7\u70b9\u5fc3\u6218\u4e8c\u95ee\u4f46\u8eab\u65b9\u5b9e\u5403\u505a\u53eb\u5f53\u4f4f\u542c\u9769\u6253\u5462\u771f\u5168\u624d\u56db\u5df2\u6240\u654c\u4e4b\u6700\u5149\u4ea7\u60c5\u8def\u5206\u603b\u6761\u767d\u8bdd\u4e1c\u5e2d\u6b21\u4eb2\u5982\u88ab\u82b1\u53e3\u653e\u513f\u5e38\u6c14\u4e94\u7b2c\u4f7f\u5199\u519b\u5427\u6587\u8fd0\u518d\u679c\u600e\u5b9a\u8bb8\u5feb\u660e\u884c\u56e0\u522b\u98de\u5916\u6811\u7269\u6d3b\u90e8\u95e8\u65e0\u5f80\u8239\u671b\u65b0\u5e26\u961f\u5148\u529b\u5b8c\u5374\u7ad9\u4ee3\u5458\u673a\u66f4\u4e5d\u60a8\u6bcf\u98ce\u7ea7\u8ddf\u7b11\u554a\u5b69\u4e07\u5c11\u76f4\u610f\u591c\u6bd4\u9636\u8fde\u8f66\u91cd\u4fbf\u6597\u9a6c\u54ea\u5316\u592a\u6307\u53d8\u793e\u4f3c\u58eb\u8005\u5e72\u77f3\u6ee1\u65e5\u51b3\u767e\u539f\u62ff\u7fa4\u7a76\u5404\u516d\u672c\u601d\u89e3\u7acb\u6cb3\u6751\u516b\u96be\u65e9\u8bba\u5417\u6839\u5171\u8ba9\u76f8\u7814\u4eca\u5176\u4e66\u5750\u63a5\u5e94\u5173\u4fe1\u89c9\u6b65\u53cd\u5904\u8bb0\u5c06\u5343\u627e\u4e89\u9886\u6216\u5e08\u7ed3\u5757\u8dd1\u8c01\u8349\u8d8a\u5b57\u52a0\u811a\u7d27\u7231\u7b49\u4e60\u9635\u6015\u6708\u9752\u534a\u706b\u6cd5\u9898\u5efa\u8d76\u4f4d\u5531\u6d77\u4e03\u5973\u4efb\u4ef6\u611f\u51c6\u5f20\u56e2\u5c4b\u79bb\u8272\u8138\u7247\u79d1\u5012\u775b\u5229\u4e16\u521a\u4e14\u7531\u9001\u5207\u661f\u5bfc\u665a\u8868\u591f\u6574\u8ba4\u54cd\u96ea\u6d41\u672a\u573a\u8be5\u5e76\u5e95\u6df1\u523b\u5e73\u4f1f\u5fd9\u63d0\u786e\u8fd1\u4eae\u8f7b\u8bb2\u519c\u53e4\u9ed1\u544a\u754c\u62c9\u540d\u5440\u571f\u6e05\u9633\u7167\u529e\u53f2\u6539\u5386\u8f6c\u753b\u9020\u5634\u6b64\u6cbb\u5317\u5fc5\u670d\u96e8\u7a7f\u5185\u8bc6\u9a8c\u4f20\u4e1a\u83dc\u722c\u7761\u5174\u5f62\u91cf\u54b1\u89c2\u82e6\u4f53\u4f17\u901a\u51b2\u5408\u7834\u53cb\u5ea6\u672f\u996d\u516c\u65c1\u623f\u6781\u5357\u67aa\u8bfb\u6c99\u5c81\u7ebf\u91ce\u575a\u7a7a\u6536\u7b97\u81f3\u653f\u57ce\u52b3\u843d\u94b1\u7279\u56f4\u5f1f\u80dc\u6559\u70ed\u5c55\u5305\u6b4c\u7c7b\u6e10\u5f3a\u6570\u4e61\u547c\u6027\u97f3\u7b54\u54e5\u9645\u65e7\u795e\u5ea7\u7ae0\u5e2e\u5566\u53d7\u7cfb\u4ee4\u8df3\u975e\u4f55\u725b\u53d6\u5165\u5cb8\u6562\u6389\u5ffd\u79cd\u88c5\u9876\u6025\u6797\u505c\u606f\u53e5\u533a\u8863\u822c\u62a5\u53f6\u538b\u6162\u53d4\u80cc\u7ec6";
		int x = 25;
		int y = 25;
		//设置字体的颜色和大小
		g2d.setColor(Color.yellow);
		g2d.setFont(new Font("宋体",Font.BOLD,20));
		Random r = new Random();
		for(int i=0;i<4;i++) {
			
			int len = r.nextInt(words.length());
			//根据位置得到字符
			char ch = words.charAt(len);
			//旋转的角度是+-30度
			int jiaodu = r.nextInt(60)-30;
			//计算弧度
			double hudu = jiaodu*Math.PI/180;
			//进行旋转
			g2d.rotate(hudu, x, y);
			
			//把数字和字母画到图片上
			g2d.drawString(ch+"", x, y);
			//转回来
			g2d.rotate(-hudu, x, y);
			x += 30;
			
		}

		g2d.setColor(Color.green);
		//生成三条干扰线 drawLine(int x1, int y1, int x2, int y2) 
		for(int j=0;j<3;j++) {
			//生成随机的宽 x
			int x1 = r.nextInt(width);
			int y1 = r.nextInt(height);
			int x2 = r.nextInt(width);
			int y2 = r.nextInt(height);
			g2d.drawLine(x1, y1, x2, y2);
		}
		
		
		//显示图片到页面上
		ImageIO.write(bufferedImage, "jpg", response.getOutputStream());
	}

	/**
	 * 
	 */
	public void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		doGet(request, response);
	}








package cn.itcast.utils;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ResourceBundle;

public class MyJdbcUtils {
	/*
	 * 把数据库的相关的信息通过读取配置文件的方式得到
	 * 
	 * * 在类加载的时候，得到这些数据库的信息
	 * */
	
	public static String drivername;
	public static String url;
	public static String username;
	public static String password;
	
	static {
		//读取配置文件把这些参数赋值
		drivername = ResourceBundle.getBundle("db").getString("drivername");
		url = ResourceBundle.getBundle("db").getString("url");
		username = ResourceBundle.getBundle("db").getString("username");
		password = ResourceBundle.getBundle("db").getString("password");
	}
	
	//获取数据库连接的方法
	public static Connection getConnection() {
		try {
			//加载驱动
			Class.forName(drivername);
			Connection conn = DriverManager.
					getConnection(url, username, password);
			return conn;
		}catch(Exception e) {
			return null;
		}
	}
	
	//释放资源的方法
	public static void clear1(ResultSet rs,Statement stmt,Connection conn) {
		if(rs != null) {
			try {
				rs.close();
			} catch (SQLException e) {
			}
			rs = null;
		}
		if(stmt != null) {
			try {
				stmt.close();
			} catch (SQLException e) {
			}
			stmt = null;
		}
		if(conn != null) {
			try {
				conn.close();
			} catch (SQLException e) {
			}
			conn = null;
		}		
	}
	
	//释放资源的方法
	public static void clear1(Statement stmt,Connection conn) {
		if(stmt != null) {
			try {
				stmt.close();
			} catch (SQLException e) {
			}
			stmt = null;
		}
		if(conn != null) {
			try {
				conn.close();
			} catch (SQLException e) {
			}
			conn = null;
		}		
	}
}














package cn.itheima.upload;

import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.util.List;
import java.util.UUID;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.apache.commons.fileupload.FileItem;
import org.apache.commons.fileupload.disk.DiskFileItemFactory;
import org.apache.commons.fileupload.servlet.ServletFileUpload;

public class UploadServlet extends HttpServlet {

	/**
	 * 	第一步：创建一个磁盘文件项工厂
		** 使用DiskFileItemFactory类，new DiskFileItemFactory()创建工厂
		第二步：创建一个核心的上传类
			** 使用ServletFileUpload类，new ServletFileUpload(FileItemFactory fileItemFactory)
		第三步：使用核心上传类解析request对象
			** 使用ServletFileUpload类里面的方法parseRequest(javax.servlet.http.HttpServletRequest request)
			** 返回的是list集合，在集合里面有泛型是FileItem，
			*** 在提交的表单里面，可能有普通输入项和文件上传项，会有多个，每个都是使用FileItem，多个项构成
			了一个list集合
		第四步：返回list集合，判断普通输入项还是文件上传项
			** 遍历list集合，判断普通输入项还是文件上传项 isFormField()
		第五步：如果是普通输入项，获取输入的值；如果是文件上传项，写上传的代码
	 */
	public void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		try {
			//创建一个磁盘文件项工厂
			DiskFileItemFactory fileItemFactory = new DiskFileItemFactory();
			//设置缓冲区的大小和临时文件存储路径
			fileItemFactory.setSizeThreshold(1*1024*1024); //字节  1*1024*1024
			//得到temp完全路径
			String temp = getServletContext().getRealPath("/temp");
			//当上传的文件超过缓冲区的大小产生临时文件
			fileItemFactory.setRepository(new File(temp));
			
			//创建核心上传类
			ServletFileUpload fileUpload = new ServletFileUpload(fileItemFactory);
			//设置上传文件的大小
//			fileUpload.setFileSizeMax(1*1024*1024);//字节
			//设置上传中文文件名称的编码
			fileUpload.setHeaderEncoding("utf-8");
			//解析request对象
			List<FileItem> list = fileUpload.parseRequest(request);
			//遍历list集合，得到普通输入项和文件上传项
			for(FileItem fileItem : list) {
				//判断普通输入项还是文件上传项
				if(fileItem.isFormField()) {//普通输入项
					//获取普通输入项的值
					//获取普通输入项的name的值
					String name = fileItem.getFieldName();
					String value = fileItem.getString("utf-8");
					System.out.println(name+" :: "+value);
				} else {//文件上传项
					//写上传的代码
					//得到上传文件的名称
					String filename = fileItem.getName();
					//使用getName方法得到文件名称，在某些浏览器下面得到的带路径地址 c:\test\1.txt
					int lens = filename.lastIndexOf("\\");
					//判断
					if(lens != -1) {
						//截取的操作
						filename = filename.substring(lens+1);
					}
					//在文件名里面添加随机的字符串     随机字符串_文件名称
					//生成随机字符串
					String uuid = UUID.randomUUID().toString();
					filename = uuid+"_"+filename;
					
					//把表单提交过来的文件写到服务器路径下面
					//使用输入流得到提交过来的文件
					InputStream in = fileItem.getInputStream();
					//得到upload的完全路径
					String path = getServletContext().getRealPath("/upload");					
					OutputStream out = new FileOutputStream(path+"/"+filename);
					//流对接
					int len = 0;
					byte[] b = new byte[1024];
					while((len=in.read(b))!=-1) {
						out.write(b, 0, len);
					}
					in.close();
					out.close();
					//删除临时文件
					fileItem.delete();
				}
			}
		} catch(Exception e) {
			e.printStackTrace();
		}
	}

	/**
	 * 
	 */
	public void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		doGet(request, response);
	}

}
