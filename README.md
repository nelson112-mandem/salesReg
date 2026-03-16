# salesReg[SalesRecordSystem.java](https://github.com/user-attachments/files/26030672/SalesRecordSystem.java)
import javax.swing.*;
import javax.swing.table.DefaultTableModel;
import java.awt.*;
import java.time.LocalTime;
import java.time.format.DateTimeFormatter;
import java.util.HashMap;
import java.util.Map;

public class SalesRecordSystem extends JFrame {
    private final DefaultTableModel salesTableModel;
    private final JTable salesTable;
    private final JTextField productField;
    private final JTextField quantityField;
    private final JTextField priceField;
    private final JComboBox<String> paymentMethodBox;
    private final JLabel totalSalesLabel;
    private final JLabel cashTotalLabel;
    private final JLabel mobileTotalLabel;
    private final JLabel clockLabel; // NEW clock label

    private double totalSales = 0.0;
    private double cashTotal = 0.0;
    private double mobileTotal = 0.0;

    private final DefaultTableModel summaryTableModel;
    private final JTable summaryTable;
    private final Map<String, double[]> dailyTotals = new HashMap<>();


    public SalesRecordSystem() {
        setTitle("Sales Record System");
        setSize(900, 600);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        JTabbedPane tabbedPane = new JTabbedPane();

        // --- Sales Entry Tab ---
        JPanel salesPanel = new JPanel(new BorderLayout());

        salesTableModel = new DefaultTableModel(
                new String[]{"Date", "Product", "Quantity", "Price", "Total", "Payment Method"}, 0
        );
        salesTable = new JTable(salesTableModel);

        productField = new JTextField(10);
        quantityField = new JTextField(5);
        priceField = new JTextField(5);
        paymentMethodBox = new JComboBox<>(new String[]{"Cash", "Mobile Money"});

        JButton addButton = new JButton("Add Sale");
        addButton.addActionListener(_ -> addSale());

        JButton exportButton = new JButton("Export to CSV");
        exportButton.addActionListener(_ -> exportToCSV());

        JButton deleteButton = new JButton("Delete Sale");
        deleteButton.addActionListener(e -> deleteSale());

        JPanel inputPanel = new JPanel();
        inputPanel.add(new JLabel("Product:"));
        inputPanel.add(productField);
        inputPanel.add(new JLabel("Quantity:"));
        inputPanel.add(quantityField);
        inputPanel.add(new JLabel("Price:"));
        inputPanel.add(priceField);
        inputPanel.add(new JLabel("Payment:"));
        inputPanel.add(paymentMethodBox);
        inputPanel.add(addButton);
        inputPanel.add(exportButton);
        inputPanel.add(deleteButton);

        totalSalesLabel = new JLabel("Total Sales: 0.00");
        cashTotalLabel = new JLabel("Cash Total: 0.00");
        mobileTotalLabel = new JLabel("Mobile Money Total: 0.00");

        JPanel totalsPanel = new JPanel(new GridLayout(1, 3));
        totalsPanel.add(totalSalesLabel);
        totalsPanel.add(cashTotalLabel);
        totalsPanel.add(mobileTotalLabel);

        salesPanel.add(inputPanel, BorderLayout.NORTH);
        salesPanel.add(new JScrollPane(salesTable), BorderLayout.CENTER);
        salesPanel.add(totalsPanel, BorderLayout.SOUTH);

        tabbedPane.addTab("Sales Entry", salesPanel);

        // --- Daily Summary Tab ---
        summaryTableModel = new DefaultTableModel(
                new String[]{"Date", "Total Sales", "Cash Sales", "Mobile Money Sales"}, 0
        );
        summaryTable = new JTable(summaryTableModel);

        JButton deleteSummaryButton = new JButton("Delete Summary Row");
        deleteSummaryButton.addActionListener(e -> deleteSummaryRow());

        JPanel summaryPanel = new JPanel(new BorderLayout());
        summaryPanel.add(new JScrollPane(summaryTable), BorderLayout.CENTER);
        summaryPanel.add(deleteSummaryButton, BorderLayout.SOUTH);

        tabbedPane.addTab("Daily Summary", summaryPanel);

        add(tabbedPane, BorderLayout.CENTER);

        // --- Status Bar with Clock ---
        clockLabel = new JLabel();
        clockLabel.setHorizontalAlignment(SwingConstants.RIGHT);
        JPanel statusBar = new JPanel(new BorderLayout());
        statusBar.add(clockLabel, BorderLayout.EAST);
        add(statusBar, BorderLayout.SOUTH);

        // Timer to update clock every second
        Timer timer = new Timer(1000, e -> updateClock());
        timer.start();
    }

    private void deleteSummaryRow() {
    }

    private void addSale() {
    }

    private void exportToCSV() {

    }

    private void deleteSale() {

    }

    private void updateClock() {
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("HH:mm:ss");
        clockLabel.setText("Current Time: " + LocalTime.now().format(formatter));
    }

    // ... keep your existing addSale, updateTotals, refreshSummaryTable, exportToCSV, deleteSale, deleteSummaryRow methods ...

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new SalesRecordSystem().setVisible(true));
    }
}
