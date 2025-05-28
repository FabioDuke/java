import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class IMCApp {

    public static void main(String[] args) {
        JFrame frame = new JFrame("Calculadora de IMC");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(400, 220);
        frame.setLocationRelativeTo(null);

        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(4, 2, 10, 10));
        panel.setBorder(BorderFactory.createEmptyBorder(20, 20, 20, 20));

        JLabel pesoLabel = new JLabel("Peso (kg):");
        JTextField pesoText = new JTextField();

        JLabel alturaLabel = new JLabel("Altura (cm):");
        JTextField alturaText = new JTextField();

        JLabel resultadoLabel = new JLabel("Resultado:");
        JLabel imcResultado = new JLabel("");

        JButton calcularButton = new JButton("Calcular");

        panel.add(pesoLabel);
        panel.add(pesoText);

        panel.add(alturaLabel);
        panel.add(alturaText);

        panel.add(resultadoLabel);
        panel.add(imcResultado);

        panel.add(new JLabel()); 
        panel.add(calcularButton);

        calcularButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                try {
                    double peso = Double.parseDouble(pesoText.getText());
                    double alturaCm = Double.parseDouble(alturaText.getText());
                    double alturaM = alturaCm / 100.0;

                    double imc = peso / (alturaM * alturaM);
                    String categoria = classificarIMC(imc);

                    imcResultado.setText(String.format("IMC: %.2f - %s", imc, categoria));
                } catch (NumberFormatException ex) {
                    JOptionPane.showMessageDialog(frame, "Insira valores numéricos válidos.",
                            "Erro de entrada", JOptionPane.ERROR_MESSAGE);
                }
            }
        });

        frame.setContentPane(panel);
        frame.setVisible(true);
    }

    private static String classificarIMC(double imc) {
        if (imc < 18.5) return "Abaixo do peso";
        else if (imc < 24.9) return "Peso normal";
        else if (imc < 29.9) return "Sobrepeso";
        else if (imc < 34.9) return "Obesidade grau I";
        else if (imc < 39.9) return "Obesidade grau II";
        else return "Obesidade grau III";
    }
}
