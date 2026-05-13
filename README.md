# Coffee App Final Project
Collaboration with Mia Payad and Maile Eusebio

## Summary
- Four drink buttons, all with different prices.
- Save Order button: Saves the drinks added.
- Load History button: Loads total price history.
- Summary button: Summarizes the order.

# Code
import javax.swing.*;
import java.awt.GridLayout;
import java.io.File;
import java.io.FileWriter;
import java.io.FileNotFoundException;
import java.io.*;
import java.util.Scanner;

public class Main{
    public static void main(String[] args) throws FileNotFoundException {

        JFrame frame = new JFrame("Cafe Shop Ordering Menu");
        JPanel panel = new JPanel(new GridLayout(4, 2, 5, 5));
        JTextArea area = new JTextArea();
        area.setEditable(false);

        JButton americano = new JButton("Americano: $4.00");
        JButton latte = new JButton("Latte: $4.50");
        JButton tea = new JButton("Black tea: $4.25");
        JButton matcha = new JButton("Matcha: $5.50");
        JButton summary = new JButton("View Summary");
        JButton save = new JButton("Save Order");
        JButton load = new JButton("Load History");

        panel.add(area);
        panel.add(americano);
        panel.add(latte);
        panel.add(tea);
        panel.add(matcha);
        panel.add(summary);
        panel.add(save);
        panel.add(load);

        final double[] total = {0};
        final String[] orderSummary = {" "};

        americano.addActionListener(e -> {
            total[0] += 4.00;
            orderSummary[0] += "Americano - $4.00\n";
            area.append("Added Americano\n");
        });

        latte.addActionListener(e -> {
            total[0] += 4.50;
            orderSummary[0] += "Latte - $4.50\n";
            area.append("Added Latte\n");
        });

        tea.addActionListener(e -> {
            total[0] += 4.25;
            orderSummary[0] += "Black tea - $4.25\n";
            area.append("Added Black tea\n");
        });

        matcha.addActionListener(e -> {
            total[0] += 5.50;
            orderSummary[0] += "Matcha - $5.50\n";
            area.append("Added Matcha\n");
        });

        summary.addActionListener(e -> {
            area.setText("--- Order Summary ---");
            area.append(orderSummary[0]);
            area.append("\nTotal: $" + String.format("%.2f", total[0]));
        });

        save.addActionListener(e -> {

            try{

                FileWriter writer = new FileWriter("order_history.txt");
                writer.write("--- New Order ---\n");
                writer.write("Total: $" + String.format("%.2f", total[0]) + "\n\n");
                writer.close();

                area.append("\nOrder Saved\n");
            } catch(IOException ex) {
                area.append("\nError Saving File\n");
            }
        });

        load.addActionListener(e -> {

            try{
                 Scanner reader = new Scanner(new File("order_history.txt"));
                 area.setText("--- Order History ---");
                 while(reader.hasNextLine()){
                     area.append(reader.nextLine() + "\n");
                 }
                 reader.close();
            } catch(IOException ex){
                area.append("\nNo Order History Found\n");
            }
        });

    frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    frame.add(panel);
    frame.setSize(800,500);
    frame.setVisible(true);
    }
}
