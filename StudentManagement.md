package test;

import java.awt.BorderLayout;
import java.awt.EventQueue;

import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.border.EmptyBorder;

import com.mysql.jdbc.Connection;
import com.mysql.jdbc.Driver;
import com.mysql.jdbc.Statement;

import javax.swing.JLabel;
import javax.swing.JOptionPane;

import java.awt.Font;
import javax.swing.JTextField;
import javax.swing.JRadioButton;
import javax.swing.JButton;
import java.awt.event.ActionListener;
import java.sql.DriverManager;
import java.awt.event.ActionEvent;

public class studentmanagement extends JFrame {

	private JPanel contentPane;
	private JTextField tfEmail;
	private JTextField tfPassword;
	private java.sql.Connection conn;
	private java.sql.Statement st;
	
	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					studentmanagement frame = new studentmanagement();
					frame.setVisible(true);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}
// ham connectdb
	public void ConnectDB()
	{
		try {
			Class.forName("com.mysql.jdbc.Driver");
			conn =DriverManager.getConnection("jdbc:mysql://localhost/studentdb", "root", "");
			System.out.println("Connect Sucess");
			
		} catch (Exception e) {
			// TODO: handle exception
			e.printStackTrace();
		}
	}
	/**
	 * Create the frame.
	 */
	public studentmanagement() {
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(100, 100, 550, 346);
		contentPane = new JPanel();
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		setContentPane(contentPane);
		contentPane.setLayout(null);
		
		JLabel lblStudentForm = new JLabel("Student Form");
		lblStudentForm.setFont(new Font("Tahoma", Font.PLAIN, 20));
		lblStudentForm.setToolTipText("");
		lblStudentForm.setBounds(226, 11, 131, 54);
		contentPane.add(lblStudentForm);
		
		JLabel lblEmail = new JLabel("Email");
		lblEmail.setFont(new Font("Tahoma", Font.PLAIN, 15));
		lblEmail.setBounds(95, 89, 46, 14);
		contentPane.add(lblEmail);
		
		tfEmail = new JTextField();
		tfEmail.setFont(new Font("Times New Roman", Font.PLAIN, 11));
		tfEmail.setBounds(204, 89, 157, 20);
		contentPane.add(tfEmail);
		tfEmail.setColumns(10);
		
		JLabel lblPassword = new JLabel("Password ");
		lblPassword.setFont(new Font("Tahoma", Font.PLAIN, 15));
		lblPassword.setBounds(95, 134, 81, 14);
		contentPane.add(lblPassword);
		
		tfPassword = new JTextField();
		tfPassword.setBounds(204, 133, 158, 20);
		contentPane.add(tfPassword);
		tfPassword.setColumns(10);
		
		JRadioButton rdoMale = new JRadioButton("Male");
		rdoMale.setBounds(204, 186, 109, 23);
		contentPane.add(rdoMale);
		
		JRadioButton rdoFemale = new JRadioButton("Female");
		rdoFemale.setBounds(315, 186, 109, 23);
		contentPane.add(rdoFemale);
		
		JLabel lblGender = new JLabel("Gender");
		lblGender.setFont(new Font("Tahoma", Font.PLAIN, 15));
		lblGender.setBounds(95, 188, 67, 14);
		contentPane.add(lblGender);
		
		JButton btnRegist = new JButton("AddNew");
		btnRegist.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {
				try {
					String gt="";
					if(rdoMale.isSelected()) gt=rdoMale.getText();
					if(rdoFemale.isSelected()) gt=rdoFemale.getText();
					ConnectDB();
					st = conn.createStatement();
					int n = st.executeUpdate("Insert into account values('"+tfEmail.getText()+"','"+tfPassword.getText()+"','"+gt+"')");
					if(n>0) JOptionPane.showMessageDialog(null, "Success");
					else JOptionPane.showMessageDialog(null, "Fail");

				} catch (Exception e) {
					// TODO: handle exception
					e.printStackTrace();
	
				}
			}
		});
		btnRegist.setBounds(95, 244, 89, 23);
		contentPane.add(btnRegist);
		
		JButton btnUpdate = new JButton("Update");
		btnUpdate.setBounds(226, 244, 89, 23);
		contentPane.add(btnUpdate);
		
		JButton btnDelete = new JButton("Delete");
		btnDelete.setBounds(363, 244, 89, 23);
		contentPane.add(btnDelete);
	}
}
