# CRUD-OPERATION


package com.controller;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.List;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

import com.dao.accountdao;
import com.pojo.account;

@WebServlet("/AccountServlet")
public class accountservlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
    accountdao ad=new accountdao(); 
    account a=new account();
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
//		PrintWriter out =response.getWriter();
		HttpSession sesion=request.getSession();
		List<account> alist=ad.getaccountlist();
		sesion.setAttribute("acclist",	 alist);
	System.out.println(alist);
		response.sendRedirect("accountlist.jsp");
		

	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		
		String accountNo=request.getParameter("accno");
		String bankName=request.getParameter("bname");
		String ifscCode=request.getParameter("ifsc");
		int salary=Integer.parseInt(request.getParameter("salary"));
		String salaryDate=request.getParameter("sdate");
		System.out.println(accountNo+"   "+bankName+"   "+ifscCode+"   "+salary+"    "+salaryDate);
		a.setAccountNo(accountNo);a.setBankName(bankName);a.setIfscCode(ifscCode);
		a.setSalary(salary);a.setSalaryDate(salaryDate);
		boolean b=ad.addAccount(a);
		if(b) {
			response.sendRedirect("index.html");
		}else {
			response.sendRedirect("error.html");
		}
		
	}

}
