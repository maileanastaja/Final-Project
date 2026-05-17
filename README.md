# Coffee App Final Project
Collaboration with Mia Payad and Maile Eusebio

## Summary
- Four drink buttons, all with different prices.
- Save Order button: Saves the drinks added.
- Load History button: Loads total price history.
- Summary button: Summarizes the order.

# Code
```
import javax.swing.*;
import java.awt.*;
import java.io.*;
import java.util.Scanner;

public class Main{
    public static void main(String[]args){

        String [] order = {""};
        double[] total= {0.0};

        JFrame frame= new JFrame("Coffee Shop");
        JPanel panel= new JPanel(new GridLayout(4,2,5,5));

        JLabel label= new JLabel("Select your drink: ");
        JTextArea orderArea= new JTextArea();
        orderArea.setEditable(false);

        JScrollPane scrollPane = new JScrollPane(orderArea);


        JLabel totalLabel= new JLabel("Total: $0.00");

        JButton americanoBtn= new JButton("Americano: $4.00");
        JButton latteBtn= new JButton("Latte: $4.50");
        JButton teaBtn= new JButton("Tea: $4.25");
        JButton matchaBtn= new JButton("Matcha: $5.50");
        JButton saveBtn= new JButton("Save Order");
        JButton loadBtn= new JButton("Load History");

        americanoBtn.addActionListener(e->{
            order[0] += "Americano\n";
            total[0] += 4.00;
            orderArea.setText("Total: $" +String.format("%.2f", total[0]));
            totalLabel.setText("Total = $" + total[0]);

            orderArea.setCaretPosition(orderArea.getDocument().getLength());
        });
        latteBtn.addActionListener(e->{
            order[0] += "Latte\n";
            total[0] += 4.25;
            orderArea.setText("Total: $" +String.format("%.2f", total[0]));
            totalLabel.setText("Total = $" + total[0]);

            orderArea.setCaretPosition(orderArea.getDocument().getLength());
        });
        teaBtn.addActionListener(e->{
            order[0] += "Tea\n";
            total[0] += 4.25;
            orderArea.setText("Total: $" +String.format("%.2f", total[0]));
            totalLabel.setText("Total = $" + total[0]);

            orderArea.setCaretPosition(orderArea.getDocument().getLength());
        });
        matchaBtn.addActionListener(e-> {
            order[0] += "Matcha\n";
            total[0] += 5.50;
            orderArea.setText("Total: $" + String.format("%.2f", total[0]));
            totalLabel.setText("Total = $" + total[0]);

            orderArea.setCaretPosition(orderArea.getDocument().getLength());
        });
        saveBtn.addActionListener(e->{
            try{
                FileWriter writer = new FileWriter("orders.text", true);

                writer.write("New Order: \n");
                writer.write(order[0]);
                writer.write("Total: $"+ total[0] + "\n");
                writer.write("---------------\n");
                writer.close();
                label.setText("Order Saved!");

            } catch(IOException ex){
                label.setText("Error saving order.");
            }
        });
        loadBtn.addActionListener(e->{
            try{
                File file= new File("orders.text");
                Scanner reader= new Scanner(file);

                orderArea.setText("Order History: \n");
                while(reader.hasNextLine()){
                    orderArea.append(reader.nextLine()+ "\n");
                }

                orderArea.setCaretPosition(orderArea.getDocument().getLength());

                reader.close();
            }catch(FileNotFoundException ex){
                label.setText("No history found.");
            }
        });

        panel.add(label);
        panel.add(scrollPane);
        panel.add(totalLabel);
        panel.add(americanoBtn);
        panel.add(latteBtn);
        panel.add(teaBtn);
        panel.add(matchaBtn);
        panel.add(saveBtn);
        panel.add(loadBtn);

        frame.add(panel);

        frame.setSize(300,400);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);

    }
}
```
