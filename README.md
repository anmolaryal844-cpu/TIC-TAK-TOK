import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class TicTacToeGUI implements ActionListener {

    JFrame frame;
    JButton[][] buttons = new JButton[3][3];
    JLabel status;
    char player = 'X';

    public TicTacToeGUI() {
        frame = new JFrame("Tic Tac Toe");
        frame.setSize(400, 450);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setLayout(new BorderLayout());

        status = new JLabel("Player X Turn", SwingConstants.CENTER);
        status.setFont(new Font("Arial", Font.BOLD, 20));
        frame.add(status, BorderLayout.NORTH);

        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(3, 3));

        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                buttons[i][j] = new JButton("");
                buttons[i][j].setFont(new Font("Arial", Font.BOLD, 40));
                buttons[i][j].addActionListener(this);
                panel.add(buttons[i][j]);
            }
        }

        frame.add(panel, BorderLayout.CENTER);
        frame.setVisible(true);
    }

    public void actionPerformed(ActionEvent e) {
        JButton btn = (JButton) e.getSource();

        if (!btn.getText().equals("")) return;

        btn.setText(String.valueOf(player));

        if (checkWin()) {
            status.setText("Player " + player + " Wins!");
            disableButtons();
        } else {
            player = (player == 'X') ? 'O' : 'X';
            status.setText("Player " + player + " Turn");
        }
    }

    boolean checkWin() {
        for (int i = 0; i < 3; i++) {
            if (same(buttons[i][0], buttons[i][1], buttons[i][2])) return true;
            if (same(buttons[0][i], buttons[1][i], buttons[2][i])) return true;
        }
        return same(buttons[0][0], buttons[1][1], buttons[2][2]) ||
               same(buttons[0][2], buttons[1][1], buttons[2][0]);
    }

    boolean same(JButton a, JButton b, JButton c) {
        return !a.getText().equals("") &&
               a.getText().equals(b.getText()) &&
               b.getText().equals(c.getText());
    }

    void disableButtons() {
        for (int i = 0; i < 3; i++)
            for (int j = 0; j < 3; j++)
                buttons[i][j].setEnabled(false);
    }

    public static void main(String[] args) {
        new TicTacToeGUI();
    }
}

