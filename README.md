# Calculator
Este es un código para java con el cual pueden crear una calculadora :

// Calculator.java //

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Calculator extends JFrame {
    private JTextField display;
    private double number1, number2, result;
    private String operation;

    public Calculator() {
        // Configurar la ventana
        setTitle("Calculadora");
        setSize(250, 250);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        // Crear la pantalla de visualización
        display = new JTextField(20);
        display.setEditable(false);
        display.setFont(new Font("Arial", Font.BOLD, 24));
        display.setHorizontalAlignment(JTextField.RIGHT);
        add(display, BorderLayout.NORTH);

        // Crear los botones numéricos
        JPanel numericPanel = new JPanel(new GridLayout(4, 3));
        numericPanel.setBorder(BorderFactory.createTitledBorder("Números"));
        for (int i = 0; i <= 9; i++) {
            JButton button = new JButton(String.valueOf(i));
            button.addActionListener(new NumericButtonListener());
            numericPanel.add(button);
        }
        add(numericPanel, BorderLayout.CENTER);

        // Crear los botones de operaciones
        JPanel operationPanel = new JPanel(new GridLayout(1, 4));
        operationPanel.setBorder(BorderFactory.createTitledBorder("Operaciones"));
        JButton addButton = new JButton("+");
        addButton.addActionListener(new OperationButtonListener("+"));
        operationPanel.add(addButton);

        JButton subtractButton = new JButton("-");
        subtractButton.addActionListener(new OperationButtonListener("-"));
        operationPanel.add(subtractButton);

        JButton multiplyButton = new JButton("*");
        multiplyButton.addActionListener(new OperationButtonListener("*"));
        operationPanel.add(multiplyButton);

        JButton divideButton = new JButton("/");
        divideButton.addActionListener(new OperationButtonListener("/"));
        operationPanel.add(divideButton);

        add(operationPanel, BorderLayout.EAST);

        // Crear el panel de botones de igualdad y limpieza
        JPanel buttonPanel = new JPanel(new GridLayout(1, 2));
        buttonPanel.setBorder(BorderFactory.createTitledBorder("Acciones"));
        JButton equalsButton = new JButton("=");
        equalsButton.addActionListener(new EqualsButtonListener());
        buttonPanel.add(equalsButton);

        JButton clearButton = new JButton("C");
        clearButton.addActionListener(new ClearButtonListener());
        buttonPanel.add(clearButton);

        add(buttonPanel, BorderLayout.SOUTH);

        // Mostrar la ventana
        setVisible(true);
    }

    private class NumericButtonListener implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            String text = display.getText();
            text += ((JButton) e.getSource()).getText();
            display.setText(text);
        }
    }

    private class OperationButtonListener implements ActionListener {
        private String operation;

        public OperationButtonListener(String operation) {
            this.operation = operation;
        }

        @Override
        public void actionPerformed(ActionEvent e) {
            number1 = Double.parseDouble(display.getText());
            Calculator.this.operation = operation;
            display.setText("");
        }
    }

    private class EqualsButtonListener implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            number2 = Double.parseDouble(display.getText());
            switch (operation) {
                case "+":
                    result = number1 + number2;
                    break;
                case "-":
                    result = number1 - number2;
                    break;
                case "*":
                    result = number1 * number2;
                    break;
                case "/":
                    if (number2 != 0) {
                        result = number1 / number2;
                    } else {
                        display.setText("Error: División por cero");
                        return;
                    }
                    break;
            }
            display.setText(String.valueOf(result)); // Mostrar el resultado en la pantalla de visualización
        }
    }

    private class ClearButtonListener implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            display.setText("");
        }
    }

    public static void main(String[] args) {
        new Calculator();
    }
}
    public static void main(String[] args) {
        new Calculator();
    }
}
