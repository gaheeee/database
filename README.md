# database

  try {
			    String strDate = "20211215";
				SimpleDateFormat dtFormat = new SimpleDateFormat("yyyyMMdd");
				SimpleDateFormat newDtFormat = new SimpleDateFormat("yyyy-MM-dd-E요일");
				Date formatDate = dtFormat.parse(strDate);
				String strNewDtFormat = newDtFormat.format(formatDate);
				System.out.println("현재 날짜 : " + strNewDtFormat);
		   }
		   catch (ParseException e) {
				e.printStackTrace();
			}


import java.text.SimpleDateFormat;
import java.util.Date;
import java.text.ParseException;


			   jframe.addWindowListener(new WindowAdapter() {
			       public void windowClosing(WindowEvent windowEvent) {
			    	   try {
			    	       con.close();
			    	       System.out.println("프로그램 종료");
			    	   } catch (SQLException a) {
			    	       a.printStackTrace();
			    	   }
			       }
			   });

-새창열기
https://dinae.tistory.com/27

private class admin_chang extends JFrame{
    	admin_chang(){
    		super("관리자창");
    		JPanel panel = new JPanel();
    		setSize(600,500);
    		
    		add(panel);
    		
    		Dimension frameSize = getSize();
            Dimension windowSize = Toolkit.getDefaultToolkit().getScreenSize();
            
            //setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
            setVisible(true);
    	}
    }


        btn_admin.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                new Part1();
                
            }
        });
        
        btn_login.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                new Part1();
                
            }
        });
	
	
	btn_reset.addActionListener(new ActionListener(){
		           public void actionPerformed(ActionEvent e){
		           	  try { 
		           	  Statement stmt=con.createStatement();
		           	  
		              stmt.execute("DROP TABLE ticket;");
		              stmt.execute("DROP TABLE seat;");
		              stmt.execute("DROP TABLE schedule;");
		              stmt.execute("DROP TABLE book;");
		              stmt.execute("DROP TABLE customer;");
		              stmt.execute("DROP TABLE room;");
		              stmt.execute("DROP TABLE movie_info;");
		              

		              stmt.execute("CREATE TABLE IF NOT EXISTS movie_info (  movie_id INT NOT NULL,    movie_name VARCHAR(45) NOT NULL,  movie_runtime INT NOT NULL,  movie_grade VARCHAR(10) NOT NULL,  \r\n"
		              		+ "  movie_director VARCHAR(45) NOT NULL,  movie_actor VARCHAR(45) NOT NULL,  movie_genre VARCHAR(45) NOT NULL,  movie_date DATE NOT NULL,  movie_intro VARCHAR(100) NOT NULL,  PRIMARY KEY (movie_id));");
		              stmt.execute("CREATE TABLE IF NOT EXISTS room (  room_id INT NOT NULL,  room_seat INT NOT NULL,  room_use VARCHAR(1) NOT NULL,  PRIMARY KEY (room_id));");
		              stmt.execute("CREATE TABLE IF NOT EXISTS customer (  customer_id VARCHAR(45) NOT NULL,  customer_name VARCHAR(45) NOT NULL,  customer_phone VARCHAR(45) NULL,\r\n"
		              		+ "  customer_mail VARCHAR(45) NULL,  PRIMARY KEY (customer_id),  UNIQUE INDEX customer_mail_UNIQUE (customer_mail ASC) VISIBLE);");
		              stmt.execute("CREATE TABLE IF NOT EXISTS book (  book_id INT NOT NULL,  book_payway VARCHAR(45) NOT NULL,  book_state VARCHAR(45) NOT NULL,  book_total INT NOT NULL,  customer_id VARCHAR(45) NOT NULL,\r\n"
		              		+ "  book_date DATE NOT NULL,  PRIMARY KEY (book_id),  CONSTRAINT customer_id    FOREIGN KEY (customer_id)    REFERENCES customer (customer_id)    ON DELETE NO ACTION    ON UPDATE NO ACTION);");
		              stmt.execute("CREATE TABLE IF NOT EXISTS schedule (  schedule_id INT NOT NULL,  movie_id INT NOT NULL,  room_id INT NOT NULL,  schedule_start DATE NOT NULL,  schedule_day VARCHAR(45) NOT NULL,  schedule_num INT NOT NULL,  \r\n"
		              		+ "  schedule_time VARCHAR(45) NOT NULL,  PRIMARY KEY (schedule_id),  INDEX movie_id_idx (movie_id ASC) VISIBLE,    INDEX room_id_idx (room_id ASC) VISIBLE,  CONSTRAINT movie_id  FOREIGN KEY (movie_id)    \r\n"
		              		+ "  REFERENCES movie_info (movie_id)    ON DELETE NO ACTION    ON UPDATE NO ACTION,  CONSTRAINT room_id    FOREIGN KEY (room_id)    REFERENCES room (room_id)    ON DELETE NO ACTION    ON UPDATE NO ACTION);");
		              stmt.execute("CREATE TABLE IF NOT EXISTS seat (  seat_id INT NOT NULL,  room_id1 INT NOT NULL,  seat_use VARCHAR(1) NOT NULL,  INDEX room_id_idx (room_id1 ASC) VISIBLE,  PRIMARY KEY (seat_id, room_id1),\r\n"
		              		+ "  CONSTRAINT room_id1    FOREIGN KEY (room_id1)    REFERENCES room (room_id)    ON DELETE NO ACTION    ON UPDATE NO ACTION);");
		              stmt.execute("CREATE TABLE IF NOT EXISTS ticket (  ticket_id INT NOT NULL,  schedule_id INT NOT NULL,  room_id2 INT NOT NULL,  seat_id INT NOT NULL,  book_id INT NOT NULL,  book_use VARCHAR(1) NOT NULL,  ticket_money INT NOT NULL,\r\n"
		              		+ "  ticket_total INT NOT NULL,  PRIMARY KEY (ticket_id),  INDEX schedule_id_idx (schedule_id ASC) VISIBLE,  INDEX room_id_idx (room_id2 ASC) VISIBLE,  INDEX seat_id_idx (seat_id ASC) VISIBLE,  INDEX book_id_idx (book_id ASC) VISIBLE,\r\n"
		              		+ "  CONSTRAINT schedule_id    FOREIGN KEY (schedule_id)    REFERENCES schedule (schedule_id)    ON DELETE NO ACTION    ON UPDATE NO ACTION,  CONSTRAINT room_id2    FOREIGN KEY (room_id2)    REFERENCES room (room_id)\r\n"
		              		+ "    ON DELETE NO ACTION    ON UPDATE NO ACTION,  CONSTRAINT seat_id    FOREIGN KEY (seat_id)    REFERENCES seat (seat_id)    ON DELETE NO ACTION    ON UPDATE NO ACTION,\r\n"
		              		+ "  CONSTRAINT book_id    FOREIGN KEY (book_id)    REFERENCES book (book_id)    ON DELETE NO ACTION    ON UPDATE NO ACTION);");
		              
		             
		              stmt.execute("INSERT INTO movie_info VALUES(1, '명량', 128, 'A', '김한민', '최민식', '액션', STR_TO_DATE('2021-01-30','%Y-%m-%d'), '1597년 임진왜란 6년, 조선이야기');");
		              stmt.execute("INSERT INTO movie_info VALUES(2, '극한직업', 120, 'C', '이병헌', '류승룡', '코미디', STR_TO_DATE('2021-02-23','%Y-%m-%d'), '해체 위기를 맞는 마약반이야기');");
		              stmt.execute("INSERT INTO movie_info VALUES(3, '신과함께', 110, 'B', '김용화', '차태현', '판타지', STR_TO_DATE('2021-03-20','%Y-%m-%d'), '사후 49일 동안 7번의 재판을 거치는 판타지이야기');");
		              stmt.execute("INSERT INTO movie_info VALUES(4, '국제시장', 125, 'A', '윤제균', '황정민', '드라마', STR_TO_DATE('2021-04-17','%Y-%m-%d'), '1950년대 한국전쟁 시대이야기');");
		              stmt.execute("INSERT INTO movie_info VALUES(5, '변호인', 123, 'A', '양우석', '송강호', '드라마', STR_TO_DATE('2021-05-10','%Y-%m-%d'), '1980년대 초 부산 세무 변호사이야기');");
		              stmt.execute("INSERT INTO movie_info VALUES(6, '해운대', 130, 'D', '윤제균', '설경구', '모험', STR_TO_DATE('2021-06-08','%Y-%m-%d'), '2004년 엄청난 충격을 안겨준 인도네시아 쓰나미이야기');");
		              stmt.execute("INSERT INTO movie_info VALUES(7, '괴물', 100, 'B', '봉준호', '박해일', '모험', STR_TO_DATE('2021-07-29','%Y-%m-%d'), '한강에 나타난 정체를 알 수 없는 괴물이야기');");
		              stmt.execute("INSERT INTO movie_info VALUES(8, '베테랑', 117, 'C', '류승완', '유아인', '액션', STR_TO_DATE('2021-08-05','%Y-%m-%d'), '특수 강력사건 담당 광역수사대이야기');");
		              stmt.execute("INSERT INTO movie_info VALUES(9, '도둑들', 124, 'B', '최동훈', '김윤석', '범죄', STR_TO_DATE('2021-09-25','%Y-%m-%d'), '한 팀으로 활동 중인 한국의 도둑이야기');");
		              stmt.execute("INSERT INTO movie_info VALUES(10, '암살', 115, 'D', '최동훈', '전지현', '액션', STR_TO_DATE('2021-10-22','%Y-%m-%d'), '1933년 조국이 사라진 시대 대한민국 임시정부이야기');");
		              stmt.execute("INSERT INTO movie_info VALUES(11, '광해', 140, 'A', '추창민', '이병헌', '드라마', STR_TO_DATE('2021-11-13','%Y-%m-%d'), '붕당정치로 혼란이 극에 달한 광해군 8년이야기');");
		              stmt.execute("INSERT INTO movie_info VALUES(12, '부산행', 133, 'B', '연상호', '공유', '액션', STR_TO_DATE('2021-12-04','%Y-%m-%d'), '정체불명의 바이러스가 전국으로 확산된 대한민국이야기');");
		             
		              
		              stmt.execute("INSERT INTO room VALUES(1, 3, 'o');");
		              stmt.execute("INSERT INTO room VALUES(2, 3, 'o');");
		              stmt.execute("INSERT INTO room VALUES(3, 3, 'o');");
		              stmt.execute("INSERT INTO room VALUES(4, 3, 'o');");
		              stmt.execute("INSERT INTO room VALUES(5, 3, 'o');");
		              stmt.execute("INSERT INTO room VALUES(6, 3, 'o');");
		              stmt.execute("INSERT INTO room VALUES(7, 3, 'o');");
		              stmt.execute("INSERT INTO room VALUES(8, 3, 'o');");
		              stmt.execute("INSERT INTO room VALUES(9, 3, 'o');");
		              stmt.execute("INSERT INTO room VALUES(10, 3, 'o');");
		              
		              
		              stmt.execute("INSERT INTO customer VALUES('gahee', '양가희', '12345678', 'gahee@naver');");
		              stmt.execute("INSERT INTO customer VALUES('eugene', '박유진', '11112222', 'eugene@gmail');");
		              stmt.execute("INSERT INTO customer VALUES('love',   '김사랑',   '33334444',   'love@yahoo');");
		              stmt.execute("INSERT INTO customer VALUES('cheolsu', '이철수', '55556666', 'cheolsu@naver');");
		              stmt.execute("INSERT INTO customer VALUES('jisoo', '한지수', '77778888', 'jisoo@naver');");
		              stmt.execute("INSERT INTO customer VALUES('minsu', '박민수', '99991010', 'minsu@nate');");
		              stmt.execute("INSERT INTO customer VALUES('dain',   '신다인',   '98765432',  'dain@gmail');");
		              stmt.execute("INSERT INTO customer VALUES('yongsu', '김용수', '87565630', 'yong@hotmail');");
		              stmt.execute("INSERT INTO customer VALUES('junsu', '최준수', '54627877', 'junsu@yahoo');");
		              stmt.execute("INSERT INTO customer VALUES('yunju', '서윤주', '74108521', 'yunju@naver');");
		              
		              stmt.execute("INSERT INTO book VALUES (1, '카드', '완료', 10000, 'gahee', STR_TO_DATE('2021-01-31','%Y-%m-%d'));");
		              stmt.execute("INSERT INTO book VALUES (2, '카드', '완료', 10000, 'eugene', STR_TO_DATE('2021-02-24','%Y-%m-%d'));");
		              stmt.execute("INSERT INTO book VALUES (3, '카드', '완료', 10000, 'love', STR_TO_DATE('2021-03-21','%Y-%m-%d'));");
		              stmt.execute("INSERT INTO book VALUES (4, '현금', '완료', 7000, 'cheolsu', STR_TO_DATE('2021-04-18','%Y-%m-%d'));");
		              stmt.execute("INSERT INTO book VALUES (5, '현금', '완료', 7000, 'jisoo', STR_TO_DATE('2021-05-11','%Y-%m-%d'));");
		              stmt.execute("INSERT INTO book VALUES (6, '현금', '미완료', 10000, 'minsu', STR_TO_DATE('2021-06-09','%Y-%m-%d'));");
		              stmt.execute("INSERT INTO book VALUES (7, '카드', '미완료', 13000, 'dain', STR_TO_DATE('2021-07-30','%Y-%m-%d'));");
		              stmt.execute("INSERT INTO book VALUES (8, '카드', '완료', 7000, 'yongsu', STR_TO_DATE('2021-08-06','%Y-%m-%d'));");
		              stmt.execute("INSERT INTO book VALUES (9, '카드', '완료', 10000, 'junsu', STR_TO_DATE('2021-09-26','%Y-%m-%d'));");
		              stmt.execute("INSERT INTO book VALUES (10, '카드', '완료', 10000, 'yunju', STR_TO_DATE('2021-10-23','%Y-%m-%d'));");
		              
		              
		              stmt.execute("INSERT INTO schedule VALUES(1, 1, 1, STR_TO_DATE('2021-1-30','%Y-%m-%d'), '월', 1, '11:00');");
		              stmt.execute("INSERT INTO schedule VALUES(2, 2, 2, STR_TO_DATE('2021-02-23','%Y-%m-%d'), '화', 2, '12:00');");
		              stmt.execute("INSERT INTO schedule VALUES(3, 3, 3, STR_TO_DATE('2021-03-20','%Y-%m-%d'), '수', 1, '13:00');");
		              stmt.execute("INSERT INTO schedule VALUES(4, 4, 4, STR_TO_DATE('2021-04-17','%Y-%m-%d'), '목', 2, '14:00');");
		              stmt.execute("INSERT INTO schedule VALUES(5, 5, 5, STR_TO_DATE('2021-05-10','%Y-%m-%d'), '금', 1, '15:00');");
		              stmt.execute("INSERT INTO schedule VALUES(6, 6, 6, STR_TO_DATE('2021-06-08','%Y-%m-%d'), '토', 2, '16:00');");
		              stmt.execute("INSERT INTO schedule VALUES(7, 7, 7, STR_TO_DATE('2021-07-29','%Y-%m-%d'), '일', 1, '17:00');");
		              stmt.execute("INSERT INTO schedule VALUES(8, 8, 8, STR_TO_DATE('2021-08-05','%Y-%m-%d'), '월', 2, '18:00');");
		              stmt.execute("INSERT INTO schedule VALUES(9, 9, 9, STR_TO_DATE('2021-09-25','%Y-%m-%d'), '화', 1, '19:00');");
		              stmt.execute("INSERT INTO schedule VALUES(10, 10, 10, STR_TO_DATE('2021-10-22','%Y-%m-%d'), '금', 1, '20:00');");
		              stmt.execute("INSERT INTO schedule VALUES(11, 11, 1, STR_TO_DATE('2021-11-13','%Y-%m-%d'), '수', 1, '21:00');");
		              stmt.execute("INSERT INTO schedule VALUES(12, 12, 2, STR_TO_DATE('2021-12-04','%Y-%m-%d'), '목', 2, '22:00'); ");
		              
		              
		              
		              
		              JOptionPane.showMessageDialog(null, "초기화 성공.\nError Message: ");
		           	  	 
		           	  } catch(SQLException a) {
		           	  	JOptionPane.showMessageDialog(null, "초기화 실패.\nError Message: " + a);
		           	    }
		           }
		       });	


btn_movie_info.addActionListener(new ActionListener() {
	            @Override
	            public void actionPerformed(ActionEvent e) {
	                //버튼 생성
	            	JTextField tf_movie_id = new JTextField(10);
	            	tf_movie_id.add(new JLabel("movie_id"));
	            	JTextField tf_movie_name = new JTextField(10);
	            	tf_movie_name.add(new JLabel("movie_name"));
	            	JTextField tf_movie_name = new JTextField(10);
	            	tf_movie_name.add(new JLabel("movie_name"));
	            	JTextField tf_movie_name = new JTextField(10);
	            	tf_movie_name.add(new JLabel("movie_name"));
	            	JTextField tf_movie_name = new JTextField(10);
	            	tf_movie_name.add(new JLabel("movie_name"));
	                
	            }
	        });
			
						super("관리자 입력창");
			setSize(600,400);
			setLayout(new GridLayout(3,1,5,5));
			setVisible(true);
			
			
			JPanel pninsertbtn = new JPanel();
			JPanel pninserttxt = new JPanel();
			JPanel pninsertok = new JPanel();
			
			
			JButton btn_movie_info = new JButton();
			btn_movie_info.setText("movie_info");
	        
	        JButton btn_room = new JButton();
	        btn_room.setText("room");
	        
	        JButton btn_customer = new JButton();
	        btn_customer.setText("customer");
	        
	        JButton btn_book = new JButton();
	        btn_book.setText("book");
	        
	        JButton btn_schedule = new JButton();
	        btn_schedule.setText("schedule");
	        
	        JButton btn_seat = new JButton();
	        btn_seat.setText("seat");
	        
	        JButton btn_ticket = new JButton();
	        btn_ticket.setText("ticket");
	        
	        pninsertbtn.add(btn_movie_info);
	        pninsertbtn.add(btn_room);
	        pninsertbtn.add(btn_customer);
	        pninsertbtn.add(btn_book);
	        pninsertbtn.add(btn_schedule);
	        pninsertbtn.add(btn_seat);
	        pninsertbtn.add(btn_ticket);
	        
	        JButton btn_ok = new JButton();
			btn_ok.setText("입력");
			
			pninsertok.add(btn_ok);
			
			
			
			
			
	
	        
	        add(pninsertbtn);
	        add(pninserttxt);
	        add(pninsertok);
