//http://www.dreamincode.net/forums/topic/25042-creating-a-calendar-viewer-application/ 
import javax.swing.*;
import javax.swing.event.*;
import javax.swing.table.*;

import java.awt.*;
import java.awt.event.*;
import java.util.*;


public class calendar {
	static JLabel lblMonth, lblYear;
	//JLable:
	//A display area for a short text string or an image, or both

	static JButton btnPrev, btnNext;
	//JButton:
	//A button is a component the user clicks to trigger a specific action.

	static JTable tblCalendar;
	//The JTable is used to display and edit regular two-dimensional tables of cells

	static JComboBox cmbYear;
	//lets the user choose one of several choices

	static JFrame frmMain;
	//A Frame is a top-level window with a title and a border

	static Container pane;
	//Containers are the interface between a component and the low-level platform-specific 
	//functionality that supports the component. Before a web, enterprise bean, or 
	//application client component can be executed, it must be assembled into a Java EE 
	//module and deployed into its container.

	static DefaultTableModel mtblCalendar; //Table model

	static JScrollPane stblCalendar; //The scrollpane

	static JPanel pnlCalendar; //The panel

	static int realDay, realMonth, realYear, currentDay, currentMonth, currentYear;



	public static void main (String args[]) {

		try {UIManager.setLookAndFeel(UIManager.getSystemLookAndFeelClassName());}
		catch (ClassNotFoundException e) {
			System.out.println("class not found exception");
			//when the class does not exist
		}
		catch (InstantiationException e) {
			System.out.println("instantiation exception");
			//Thrown when an application tries to create an instance of a class using the 
			//newInstance method in class Class, but the specified class object cannot be 
			//instantiated
		}
		catch (IllegalAccessException e) {
			System.out.println("illegal access exception");
			//Thrown when a program attempts to access a field or method which is not 
			//accessible from the location where the reference is made.
		}
		catch (UnsupportedLookAndFeelException e) {
			System.out.println("unsupported look and feel exception");
			//An exception that indicates the requested look & feel management classes 
			//are not present on the user's system.
		}

		/* try{
			    some code that could throw  MyException;
			 }
			 catch (MyException e){
			     this will be called when MyException has occured
			 }
			 catch (Exception e){
			     this will be called if another exception has occured
			     NOT for MyException, because that is already handled above
			 }
			 finally{
			     this will always be called,
			     if there has been an exception or not
			     if there was an exception, it is called after the catch block
			 }
		 */

		frmMain = new JFrame("Calendar application");
		lblYear = new JLabel ("Year:");
		cmbYear = new JComboBox();
		JLabel lblMonth = new JLabel ("January");
		btnPrev = new JButton ("<<");
		btnNext = new JButton (">>");
		mtblCalendar = new DefaultTableModel();
		tblCalendar = new JTable(mtblCalendar); //Table using the above model
		stblCalendar = new JScrollPane(tblCalendar);
		pnlCalendar = new JPanel();
		frmMain.setSize(330, 375);
		pane = frmMain.getContentPane();
		pane.setLayout(null);
		frmMain.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		pnlCalendar.setBorder(BorderFactory.createTitledBorder("Calendar"));

		pane.add(pnlCalendar);

		pnlCalendar.add(lblMonth);

		pnlCalendar.add(lblYear);

		pnlCalendar.add(cmbYear);

		pnlCalendar.add(btnPrev);

		pnlCalendar.add(btnNext);

		pnlCalendar.add(stblCalendar);

		pnlCalendar.setBounds(0, 0, 320, 335);

		lblMonth.setBounds(160-lblMonth.getPreferredSize().width/2, 25, 100, 25);

		lblYear.setBounds(10, 305, 80, 20);

		cmbYear.setBounds(230, 305, 80, 20);

		btnPrev.setBounds(10, 25, 50, 25);

		btnNext.setBounds(260, 25, 50, 25);

		stblCalendar.setBounds(10, 50, 300, 250);

		frmMain.setResizable(false);

		frmMain.setVisible(true);


		//Get real month/year
		GregorianCalendar cal = new GregorianCalendar(); //Create calendar

		realDay = cal.get(GregorianCalendar.DAY_OF_MONTH); //Get day

		realMonth = cal.get(GregorianCalendar.MONTH); //Get month

		realYear = cal.get(GregorianCalendar.YEAR); //Get year

		currentDay = realDay;

		currentMonth = realMonth; //Match day, month, and year

		currentYear = realYear;

		for (int i=realYear-100; i<=realYear+100; i++){
			cmbYear.addItem(String.valueOf(i));
		}

		String[] headers = {"Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"}; //All headers
		for (int i=0; i<7; i++){
			mtblCalendar.addColumn(headers[i]);
		}

		tblCalendar.getParent().setBackground(tblCalendar.getBackground());
		tblCalendar.getTableHeader().setResizingAllowed(false);
		tblCalendar.getTableHeader().setReorderingAllowed(false);

		tblCalendar.setColumnSelectionAllowed(true);
		tblCalendar.setRowSelectionAllowed(true);
		tblCalendar.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);

		mtblCalendar.setRowCount(38);
		mtblCalendar.setColumnCount(7);
		mtblCalendar.setRowCount(6);

		refreshCalendar (realMonth, realYear);

	}

	public static void refreshCalendar(int month, int year){
		String[] months = {"January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"};
		int numdays, startmons;
		btnPrev.setEnabled(true);
		btnNext.setEnabled(true);
		if (month == 0 && year <= realYear-100){btnPrev.setEnabled(false);} //Too early
		if (month == 11 && year >= realYear+100){btnNext.setEnabled(false);} //Too late
		lblMonth.setText(months[month]);
		lblMonth.setBounds(160-lblMonth.getPreferredSize().width/2, 25, 180, 25);
		cmbYear.setSelectedItem(String.valueOf(year));

		 GregorianCalendar cal = new GregorianCalendar(year, month, 1);
		 numdays = cal.getActualMaximum(GregorianCalendar.DAY_OF_MONTH);
		 startmons = cal.get(GregorianCalendar.DAY_OF_WEEK);

		 
		for (int i=0; i<6; i++){
			for (int j=0; j<7; j++){
				mtblCalendar.setValueAt(null, i, j);
			}
		}
		
		for (int i=1; i<=numdays; i++){
			int row = new Integer((i+startmons-2)/7);
			int column  =  (i+startmons-2)%7;
			mtblCalendar.setValueAt(i, row, column);
		}
	}

}
