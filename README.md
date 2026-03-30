**//quiz application using swings**
package com.GQT.JavaBasics.project2;
	import javax.swing.*;
	import java.awt.event.*;
		public class quizappswings2 extends JFrame implements ActionListener {

		    JLabel questionLabel, prizeLabel;
		    JRadioButton op1, op2, op3, op4;
		    JButton submitBtn, lifelineBtn, quitBtn;

		    ButtonGroup group;

		    int index = 0;
		    int prize = 0;

		    boolean used5050 = false;
		    boolean usedAudience = false;
		    boolean usedSkip = false;

		    String questions[] = {
		            "Which company originally developed Java?",
		            "Which keyword is used to define a class in Java?",
		            "Which data type is used to store decimal numbers in Java?",
		            "Which symbol is used for single line comments in Java?",
		            "Which package contains the Scanner class?",
		            "Which loop is best when the number of iterations is known?",
		            "Which keyword is used to stop a loop in Java?",
		            "Which concept allows one class to acquire properties of another?",
		            "Which method is used to print output in Java?",
		            "Which operator is used to add two numbers?"
		    };

		    String options[][] = {
		            {"Sun Microsystems", "Microsoft", "Google", "Apple"},
		            {"class", "define", "create", "object"},
		            {"int", "float", "boolean", "char"},
		            {"//", "/* */", "#", "<!-- -->"},
		            {"java.lang", "java.util", "java.io", "java.net"},
		            {"while loop", "do while loop", "for loop", "switch"},
		            {"break", "continue", "exit", "return"},
		            {"Polymorphism", "Encapsulation", "Inheritance", "Abstraction"},
		            {"System.print()", "System.println()", "print()", "println()"},
		            {"+", "-", "*", "/"}
		    };

		    int answers[] = {0,0,1,0,1,2,0,2,1,0};

		    int rewardArray[] = {0,1000,2000,3000,4000,5000,6000,7000,8000,9000,10000};

		    quizappswings2() {

		        setTitle("GQT Quiz Game");
		        setSize(600,400);
		        setLayout(null);
		        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

		        questionLabel = new JLabel();
		        questionLabel.setBounds(50,30,500,30);
		        add(questionLabel);

		        prizeLabel = new JLabel("Prize: ₹0");
		        prizeLabel.setBounds(450,10,120,30);
		        add(prizeLabel);

		        op1 = new JRadioButton();
		        op1.setBounds(50,80,400,30);

		        op2 = new JRadioButton();
		        op2.setBounds(50,120,400,30);

		        op3 = new JRadioButton();
		        op3.setBounds(50,160,400,30);

		        op4 = new JRadioButton();
		        op4.setBounds(50,200,400,30);

		        add(op1);
		        add(op2);
		        add(op3);
		        add(op4);

		        group = new ButtonGroup();
		        group.add(op1);
		        group.add(op2);
		        group.add(op3);
		        group.add(op4);

		        submitBtn = new JButton("Submit");
		        submitBtn.setBounds(50,260,100,30);
		        submitBtn.addActionListener(this);
		        add(submitBtn);

		        lifelineBtn = new JButton("Lifeline");
		        lifelineBtn.setBounds(200,260,100,30);
		        lifelineBtn.addActionListener(this);
		        add(lifelineBtn);

		        quitBtn = new JButton("Quit");
		        quitBtn.setBounds(350,260,100,30);
		        quitBtn.addActionListener(this);
		        add(quitBtn);

		        loadQuestion();

		        setVisible(true);
		    }

		    void loadQuestion() {

		        if(index < questions.length) {

		            questionLabel.setText("Q" + (index+1) + ": " + questions[index]);

		            op1.setText(options[index][0]);
		            op2.setText(options[index][1]);
		            op3.setText(options[index][2]);
		            op4.setText(options[index][3]);

		            op1.setVisible(true);
		            op2.setVisible(true);
		            op3.setVisible(true);
		            op4.setVisible(true);

		            group.clearSelection();
		        }
		        else {

		            JOptionPane.showMessageDialog(this,"GAME OVER\nFinal Prize: ₹"+prize);
		            System.exit(0);
		        }
		    }

		    int getSelected() {

		        if(op1.isSelected()) return 0;
		        if(op2.isSelected()) return 1;
		        if(op3.isSelected()) return 2;
		        if(op4.isSelected()) return 3;

		        return -1;
		    }

		    public void actionPerformed(ActionEvent e) {

		        if(e.getSource() == submitBtn) {

		            int selected = getSelected();

		            if(selected == -1) {
		                JOptionPane.showMessageDialog(this,"Please select an option");
		                return;
		            }

		            if(selected == answers[index]) {

		                prize = rewardArray[index+1];
		                JOptionPane.showMessageDialog(this,"Correct Answer!\nYou won ₹"+prize);
		                prizeLabel.setText("Prize: ₹"+prize);

		                index++;
		                loadQuestion();
		            }
		            else {

		                JOptionPane.showMessageDialog(this,
		                        "Wrong Answer!\nCorrect Answer: "+options[index][answers[index]]
		                                +"\nYou take home ₹"+prize);

		                System.exit(0);
		            }
		        }

		        if(e.getSource() == quitBtn) {

		            JOptionPane.showMessageDialog(this,"You quit the game.\nPrize: ₹"+prize);
		            System.exit(0);
		        }

		        if(e.getSource() == lifelineBtn) {

		            String choice = JOptionPane.showInputDialog(
		                    "Choose Lifeline:\n1. 50-50\n2. Audience Poll\n3. Skip");

		            if(choice == null) return;

		            int life = Integer.parseInt(choice);

		            if(life == 1) {

		                if(!used5050) {

		                    used5050 = true;

		                    int correct = answers[index];
		                    int wrong = (correct + 1) % 4;

		                    op1.setVisible(false);
		                    op2.setVisible(false);
		                    op3.setVisible(false);
		                    op4.setVisible(false);

		                    if(correct == 0 || wrong == 0) op1.setVisible(true);
		                    if(correct == 1 || wrong == 1) op2.setVisible(true);
		                    if(correct == 2 || wrong == 2) op3.setVisible(true);
		                    if(correct == 3 || wrong == 3) op4.setVisible(true);

		                    JOptionPane.showMessageDialog(this,"50-50 activated");

		                } else {

		                    JOptionPane.showMessageDialog(this,"50-50 already used");
		                }
		            }

		            if(life == 2) {

		                if(!usedAudience) {

		                    usedAudience = true;

		                    JOptionPane.showMessageDialog(this,
		                            "Audience suggests option: "+(answers[index]+1));

		                } else {

		                    JOptionPane.showMessageDialog(this,"Audience Poll already used");
		                }
		            }

		            if(life == 3) {

		                if(!usedSkip) {

		                    usedSkip = true;

		                    JOptionPane.showMessageDialog(this,"Question Skipped");

		                    index++;
		                    loadQuestion();

		                } else {

		                    JOptionPane.showMessageDialog(this,"Skip already used");
		                }
		            }
		        }
		    }

		    public static void main(String[] args) {

		        new quizappswings2();
		    }
		}
**//quiz application using loops**
import java.util.Scanner;
public class quizapp {

	    static final String RESET = "\u001B[0m";
	    static final String RED = "\u001B[31m";
	    static final String GREEN = "\u001B[32m";
	    static final String YELLOW = "\u001B[33m";
	    static final String BLUE = "\u001B[34m";
	    static final String CYAN = "\u001B[36m";
	    static final String PURPLE = "\u001B[35m";

	    public static void main(String[] args) {

	        Scanner sc = new Scanner(System.in);

	        String questions[] = {
	                "Which company originally developed Java?",
	                "Which keyword is used to define a class in Java?",
	                "Which data type is used to store decimal numbers in Java?",
	                "Which symbol is used for single line comments in Java?",
	                "Which package contains the Scanner class?",
	                "Which loop is best when the number of iterations is known?",
	                "Which keyword is used to stop a loop in Java?",
	                "Which concept allows one class to acquire properties of another?",
	                "Which method is used to print output in Java?",
	                "Which operator is used to add two numbers?"
	        };

	        String options[][] = {
	                {"Sun Microsystems", "Microsoft", "Google", "Apple"},
	                {"class", "define", "create", "object"},
	                {"int", "float", "boolean", "char"},
	                {"//", "/* */", "#", "<!-- -->"},
	                {"java.lang", "java.util", "java.io", "java.net"},
	                {"while loop", "do while loop", "for loop", "switch"},
	                {"break", "continue", "exit", "return"},
	                {"Polymorphism", "Encapsulation", "Inheritance", "Abstraction"},
	                {"System.print()", "System.println()", "print()", "println()"},
	                {"+", "-", "*", "/"}
	        };

	        int answers[] = {0,0,1,0,1,2,0,2,1,0};

	        int rewardArray[] = {0,1000,2000,3000,4000,5000,6000,7000,8000,9000,10000};

	        int prize = 0;
	        int choice;

	        boolean used5050 = false;
	        boolean usedAudience = false;
	        boolean usedSkip = false;
	        boolean use5050now = false;

	        System.out.println(PURPLE + "--------------------------------");
	        System.out.println("          GQT QUIZ GAME         ");
	        System.out.println("--------------------------------" + RESET);

	        System.out.println(YELLOW + "Answer correctly to win money!");
	        System.out.println("Use lifelines wisely!" + RESET);

	        for(int i = 0; i < questions.length; i++) {

	            System.out.println(CYAN + "\n------------------------------------");
	            System.out.println("Question " + (i + 1) + ": " + questions[i]);
	            System.out.println("------------------------------------" + RESET);

	            int wrongOption = (answers[i] + 2) % 4;

	            for(int j = 0; j < options[i].length; j++) {

	                if(use5050now) {
	                    if(j == answers[i] || j == wrongOption) {
	                        System.out.println(BLUE + (j+1) + ". " + options[i][j] + RESET);
	                    }
	                }
	                else {
	                    System.out.println(BLUE + (j+1) + ". " + options[i][j] + RESET);
	                }
	            }

	            System.out.println(YELLOW + "5. Lifeline");
	            System.out.println("6. Quit" + RESET);

	            System.out.print("Enter your choice: ");
	            choice = sc.nextInt();

	            if(choice < 1 || choice > 6) {
	                System.out.println(RED + "Invalid choice! Try again." + RESET);
	                i--;
	                continue;
	            }

	            if(choice == 6) {
	                System.out.println(RED + "You quit the game." + RESET);
	                break;
	            }

	            if(choice == 5) {

	                if(i >= 8) {
	                    System.out.println(RED + "Lifelines are not applicable for 9 and 10 questions!" + RESET);
	                    i--;
	                    continue;
	                }

	                System.out.println(PURPLE + "Choose Lifeline:" + RESET);

	                if(!used5050)
	                    System.out.println("1. 50-50");
	                else
	                    System.out.println("1. 50-50 (Already Used)");

	                if(!usedAudience)
	                    System.out.println("2. Audience Poll");
	                else
	                    System.out.println("2. Audience Poll (Already Used)");

	                if(!usedSkip)
	                    System.out.println("3. Skip");
	                else
	                    System.out.println("3. Skip (Already Used)");

	                int life = sc.nextInt();

	                if(life == 1) {

	                    if(!used5050) {
	                        used5050 = true;
	                        use5050now = true;
	                        System.out.println(YELLOW + "50-50 activated!" + RESET);
	                    }
	                    else {
	                        System.out.println(RED + "50-50 already used!" + RESET);
	                    }

	                }
	                else if(life == 2) {

	                    if(!usedAudience) {
	                        usedAudience = true;
	                        System.out.println(YELLOW + "Audience suggests option: " + (answers[i] + 1) + RESET);
	                    }
	                    else {
	                        System.out.println(RED + "Audience Poll already used!" + RESET);
	                    }

	                }
	                else if(life == 3) {

	                    if(!usedSkip) {
	                        usedSkip = true;
	                        System.out.println(YELLOW + "Question skipped!" + RESET);
	                        continue;
	                    }
	                    else {
	                        System.out.println(RED + "Skip already used!" + RESET);
	                    }

	                }
	                else {
	                    System.out.println(RED + "Invalid lifeline choice!" + RESET);
	                }

	                i--;
	                continue;
	            }

	            if(choice - 1 == answers[i]) {

	                System.out.println(GREEN + "Correct Answer!" + RESET);
	                prize = rewardArray[i+1];
	                System.out.println(GREEN + "You won: ₹" + prize + RESET);

	            }
	            else {

	                System.out.println(RED + "Wrong Answer!" + RESET);
	                System.out.println(GREEN + "Correct Answer is: " + (answers[i] + 1) + ". " + options[i][answers[i]] + RESET);

	                if(i < 5)
	                    prize = 0;
	                else if(i < 7)
	                    prize = 5000;
	                else
	                    prize = 7000;

	                System.out.println(RED + "You take home: ₹" + prize + RESET);
	                break;
	            }

	            use5050now = false;
	        }

	        System.out.println(CYAN + "\n-----------------------------------");
	        System.out.println("            GAME OVER              ");
	        System.out.println("Final Prize: ₹" + prize);
	        System.out.println("-----------------------------------" + RESET);
	    }
	}


