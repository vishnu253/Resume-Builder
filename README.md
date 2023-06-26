I have developed a Swing GUI applictaion in INTELLIJ IDE where you can type in all the required information for your resume and select image for your resume and with just one click it develops a pdf template of your resume.

Here is the main code:
package com.company;
import com.itextpdf.text.BaseColor;
import com.itextpdf.text.Document;
import com.itextpdf.text.FontFactory;
import com.itextpdf.text.Paragraph;
import com.itextpdf.text.pdf.PdfPTable;
import com.itextpdf.text.pdf.PdfWriter;
import javax.swing.*;
import javax.swing.filechooser.FileNameExtensionFilter;
import javax.swing.plaf.FontUIResource;
import javax.swing.text.StyleContext;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.File;
import java.io.FileOutputStream;
import java.util.Locale;

    public class CV {
    private JPanel cvPanel;
    private JTextField name;
    private JTextField address;
    private JTextField contact;
    private JTextField email;
    private JTextField skills1;
    private JTextField skills2;
    private JTextField skills3;
    private JTextField skills4;
    private JComboBox work;
    private JTextField college;
    private JTextField qualiA;
    private JButton SELECTIMAGEButton;
    private JLabel img;
    private JButton GENERATERESUMEButton;
    private JTextField qualiB;
    private JTextField location;
    JFrame frame = new JFrame();

    public CV() {
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setContentPane(cvPanel);
        frame.pack();
        frame.setLocationRelativeTo(null);
        frame.setVisible(true);
        SELECTIMAGEButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                JFileChooser fileChooser = new JFileChooser();
                FileNameExtensionFilter filter = new FileNameExtensionFilter("*.IMAGE", "jpg", "png");
                fileChooser.addChoosableFileFilter(filter);
                int rs = fileChooser.showSaveDialog(null);
                if (rs == JFileChooser.APPROVE_OPTION) {
                    File selectedImage = fileChooser.getSelectedFile();
                    location.setText(selectedImage.getAbsolutePath());
                    img.setIcon(resize(location.getText()));
                }
            }
        });
        GENERATERESUMEButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                if (name.getText() == null || contact.getText() == null || address.getText() == null || email.getText() == null) {
                    JOptionPane.showMessageDialog(null, "PLEASE ENTER ALL DETAILS TO GENERATE CV");
                } else {
                    try {
                        String nameOfFile = "E:\\resume\\my.pdf";
                        Document myDocument = new Document();
                        PdfWriter.getInstance(myDocument, new FileOutputStream(nameOfFile));
                        myDocument.open();
                        com.itextpdf.text.Image img = com.itextpdf.text.Image.getInstance(location.getText());
                        img.setAbsolutePosition(473f, 750f);
                        img.scaleAbsolute(80f, 70f);
                        PdfPTable table = new PdfPTable(2);
                        myDocument.add(img);
                        myDocument.add(new Paragraph(name.getText(), FontFactory.getFont(FontFactory.TIMES_BOLD, 32, com.itextpdf.text.Font.BOLD, BaseColor.DARK_GRAY)));
                        myDocument.add(new Paragraph("", FontFactory.getFont(FontFactory.TIMES_BOLD, 9, BaseColor.DARK_GRAY)));
                        myDocument.add(new Paragraph("", FontFactory.getFont(FontFactory.TIMES_BOLD, 9, BaseColor.DARK_GRAY)));
                        myDocument.add(new Paragraph("----------------------------------------------------------------------------------------------------------------------------------"));
                        myDocument.add(new Paragraph("CONTACT DETAILS", FontFactory.getFont(FontFactory.TIMES_BOLD, 9, com.itextpdf.text.Font.BOLD, BaseColor.DARK_GRAY)));
                        myDocument.add(new Paragraph(email.getText(), FontFactory.getFont(FontFactory.TIMES_BOLD, 7, BaseColor.DARK_GRAY)));
                        myDocument.add(new Paragraph(contact.getText(), FontFactory.getFont(FontFactory.TIMES_BOLD, 7, BaseColor.DARK_GRAY)));
                        myDocument.add(new Paragraph(address.getText(), FontFactory.getFont(FontFactory.TIMES_BOLD, 7, BaseColor.DARK_GRAY)));
                        myDocument.add(new Paragraph("----------------------------------------------------------------------------------------------------------------------------------"));
                        myDocument.add(new Paragraph("SKILLS", FontFactory.getFont(FontFactory.TIMES_BOLD, 9, com.itextpdf.text.Font.BOLD, BaseColor.DARK_GRAY)));
                        table.setHeaderRows(1);
                        table.addCell(skills1.getText());
                        table.addCell(skills2.getText());
                        table.addCell(skills3.getText());
                        table.addCell(skills4.getText());
                        myDocument.add(table);
                        myDocument.add(new Paragraph("----------------------------------------------------------------------------------------------------------------------------------"));
                        myDocument.add(new Paragraph("QUALIFICATIONS", FontFactory.getFont(FontFactory.TIMES_BOLD, 9, com.itextpdf.text.Font.BOLD, BaseColor.DARK_GRAY)));
                        myDocument.add(new Paragraph(college.getText(), FontFactory.getFont(FontFactory.TIMES_BOLD, 7, BaseColor.DARK_GRAY)));
                        myDocument.add(new Paragraph(qualiA.getText(), FontFactory.getFont(FontFactory.TIMES_BOLD, 7, BaseColor.DARK_GRAY)));
                        myDocument.add(new Paragraph(qualiB.getText(), FontFactory.getFont(FontFactory.TIMES_BOLD, 7, BaseColor.DARK_GRAY)));
                        myDocument.add(new Paragraph("----------------------------------------------------------------------------------------------------------------------------------"));
                        myDocument.add(new Paragraph("WORK EXPERIENCE", FontFactory.getFont(FontFactory.TIMES_BOLD, 10, com.itextpdf.text.Font.BOLD, BaseColor.DARK_GRAY)));
                        myDocument.add(new Paragraph("" + work.getSelectedItem(), FontFactory.getFont(FontFactory.TIMES_BOLD, 7, BaseColor.DARK_GRAY)));
                        myDocument.add(new Paragraph("----------------------------------------------------------------------------------------------------------------------------------"));
                        myDocument.add(new Paragraph("REFERENCES", FontFactory.getFont(FontFactory.TIMES_BOLD, 9, com.itextpdf.text.Font.BOLD, BaseColor.DARK_GRAY)));
                        myDocument.add(new Paragraph("Available upon request", FontFactory.getFont(FontFactory.TIMES_BOLD, 6, BaseColor.DARK_GRAY)));
                        myDocument.close();
                        JOptionPane.showMessageDialog(null, "CV was successfully generated");
                    } catch (Exception ex) {
                        JOptionPane.showMessageDialog(null, ex);
                    }
                }
            }
        });
    }

    public ImageIcon resize(String path) {
        ImageIcon myImg = new ImageIcon(path);
        Image image = myImg.getImage();
        Image newImage = image.getScaledInstance(200, 200, Image.SCALE_SMOOTH);
        ImageIcon finalImage = new ImageIcon(newImage);
        return finalImage;
    }

    {
// GUI initializer generated by IntelliJ IDEA GUI Designer
// >>> IMPORTANT!! <<<
// DO NOT EDIT OR ADD ANY CODE HERE!
        $$$setupUI$$$();
    }

    /**
     * Method generated by IntelliJ IDEA GUI Designer
     * >>> IMPORTANT!! <<<
     * DO NOT edit this method OR call it in your code!
     *
     * @noinspection ALL
     */
    private void $$$setupUI$$$() {
        cvPanel = new JPanel();
        cvPanel.setLayout(new com.intellij.uiDesigner.core.GridLayoutManager(11, 6, new Insets(0, 0, 0, 0), -1, -1));
        final JLabel label1 = new JLabel();
        Font label1Font = this.$$$getFont$$$(null, -1, 14, label1.getFont());
        if (label1Font != null) label1.setFont(label1Font);
        label1.setText("Personal Information");
        cvPanel.add(label1, new com.intellij.uiDesigner.core.GridConstraints(1, 0, 1, 2, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_CENTER, com.intellij.uiDesigner.core.GridConstraints.FILL_NONE, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, null, null, 0, false));
        name = new JTextField();
        cvPanel.add(name, new com.intellij.uiDesigner.core.GridConstraints(2, 1, 3, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_HORIZONTAL, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_WANT_GROW, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, new Dimension(150, -1), null, 0, false));
        final JLabel label2 = new JLabel();
        label2.setText("Address");
        cvPanel.add(label2, new com.intellij.uiDesigner.core.GridConstraints(5, 0, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_NONE, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, null, null, 0, false));
        address = new JTextField();
        cvPanel.add(address, new com.intellij.uiDesigner.core.GridConstraints(5, 1, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_HORIZONTAL, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_WANT_GROW, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, new Dimension(150, -1), null, 0, false));
        final JLabel label3 = new JLabel();
        label3.setText("Contact");
        cvPanel.add(label3, new com.intellij.uiDesigner.core.GridConstraints(7, 0, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_NONE, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, null, null, 0, false));
        contact = new JTextField();
        cvPanel.add(contact, new com.intellij.uiDesigner.core.GridConstraints(7, 1, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_HORIZONTAL, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_WANT_GROW, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, new Dimension(150, -1), null, 0, false));
        final JLabel label4 = new JLabel();
        label4.setText("EMAIL");
        cvPanel.add(label4, new com.intellij.uiDesigner.core.GridConstraints(8, 0, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_NONE, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, null, null, 0, false));
        email = new JTextField();
        cvPanel.add(email, new com.intellij.uiDesigner.core.GridConstraints(8, 1, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_HORIZONTAL, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_WANT_GROW, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, new Dimension(150, -1), null, 0, false));
        SELECTIMAGEButton = new JButton();
        SELECTIMAGEButton.setText("SELECT IMAGE");
        cvPanel.add(SELECTIMAGEButton, new com.intellij.uiDesigner.core.GridConstraints(9, 0, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_CENTER, com.intellij.uiDesigner.core.GridConstraints.FILL_HORIZONTAL, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_CAN_SHRINK | com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_CAN_GROW, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, null, null, 0, false));
        location = new JTextField();
        cvPanel.add(location, new com.intellij.uiDesigner.core.GridConstraints(9, 1, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_HORIZONTAL, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_WANT_GROW, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, new Dimension(150, -1), null, 0, false));
        final JLabel label5 = new JLabel();
        label5.setHorizontalAlignment(0);
        label5.setText("SKILLS");
        cvPanel.add(label5, new com.intellij.uiDesigner.core.GridConstraints(1, 2, 1, 3, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_CENTER, com.intellij.uiDesigner.core.GridConstraints.FILL_NONE, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, null, null, 0, false));
        skills1 = new JTextField();
        cvPanel.add(skills1, new com.intellij.uiDesigner.core.GridConstraints(2, 2, 1, 2, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_HORIZONTAL, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_WANT_GROW, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, new Dimension(150, -1), null, 0, false));
        skills3 = new JTextField();
        cvPanel.add(skills3, new com.intellij.uiDesigner.core.GridConstraints(3, 2, 1, 2, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_HORIZONTAL, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_WANT_GROW, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, new Dimension(150, -1), null, 0, false));
        skills2 = new JTextField();
        cvPanel.add(skills2, new com.intellij.uiDesigner.core.GridConstraints(2, 5, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_HORIZONTAL, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_WANT_GROW, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, new Dimension(150, -1), null, 0, false));
        skills4 = new JTextField();
        cvPanel.add(skills4, new com.intellij.uiDesigner.core.GridConstraints(3, 5, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_HORIZONTAL, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_WANT_GROW, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, new Dimension(150, -1), null, 0, false));
        final JLabel label6 = new JLabel();
        label6.setText("Work Experience");
        cvPanel.add(label6, new com.intellij.uiDesigner.core.GridConstraints(4, 2, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_NONE, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, null, null, 0, false));
        work = new JComboBox();
        final DefaultComboBoxModel defaultComboBoxModel1 = new DefaultComboBoxModel();
        defaultComboBoxModel1.addElement("> 1 yrs");
        defaultComboBoxModel1.addElement("2 yrs");
        defaultComboBoxModel1.addElement("3 yrs");
        defaultComboBoxModel1.addElement("4 yrs");
        defaultComboBoxModel1.addElement("5+ yrs");
        work.setModel(defaultComboBoxModel1);
        cvPanel.add(work, new com.intellij.uiDesigner.core.GridConstraints(4, 3, 1, 2, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_HORIZONTAL, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_CAN_GROW, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, null, null, 0, false));
        final JLabel label7 = new JLabel();
        label7.setText("Full Name");
        cvPanel.add(label7, new com.intellij.uiDesigner.core.GridConstraints(3, 0, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_NONE, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, null, null, 0, false));
        final JLabel label8 = new JLabel();
        label8.setText("Qualification 1");
        cvPanel.add(label8, new com.intellij.uiDesigner.core.GridConstraints(7, 2, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_NONE, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, null, null, 0, false));
        qualiA = new JTextField();
        qualiA.setText("");
        cvPanel.add(qualiA, new com.intellij.uiDesigner.core.GridConstraints(7, 3, 1, 2, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_HORIZONTAL, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_WANT_GROW, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, new Dimension(150, -1), null, 0, false));
        final JLabel label9 = new JLabel();
        label9.setText("Qualification 2");
        cvPanel.add(label9, new com.intellij.uiDesigner.core.GridConstraints(8, 2, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_NONE, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, null, null, 0, false));
        qualiB = new JTextField();
        cvPanel.add(qualiB, new com.intellij.uiDesigner.core.GridConstraints(8, 3, 1, 2, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_HORIZONTAL, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_WANT_GROW, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, new Dimension(150, -1), null, 0, false));
        final JLabel label10 = new JLabel();
        label10.setText("College/University");
        cvPanel.add(label10, new com.intellij.uiDesigner.core.GridConstraints(6, 2, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_NONE, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, null, null, 0, false));
        college = new JTextField();
        cvPanel.add(college, new com.intellij.uiDesigner.core.GridConstraints(6, 3, 1, 2, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_HORIZONTAL, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_WANT_GROW, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, new Dimension(150, -1), null, 0, false));
        GENERATERESUMEButton = new JButton();
        GENERATERESUMEButton.setText("GENERATE RESUME");
        cvPanel.add(GENERATERESUMEButton, new com.intellij.uiDesigner.core.GridConstraints(10, 2, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_CENTER, com.intellij.uiDesigner.core.GridConstraints.FILL_HORIZONTAL, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_CAN_SHRINK | com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_CAN_GROW, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, null, null, 0, false));
        final JLabel label11 = new JLabel();
        Font label11Font = this.$$$getFont$$$(null, -1, 18, label11.getFont());
        if (label11Font != null) label11.setFont(label11Font);
        label11.setText("             CV BUILDER");
        cvPanel.add(label11, new com.intellij.uiDesigner.core.GridConstraints(0, 2, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_CENTER, com.intellij.uiDesigner.core.GridConstraints.FILL_NONE, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, null, null, 0, false));
        final JLabel label12 = new JLabel();
        label12.setText("QUALIFICATIONS");
        cvPanel.add(label12, new com.intellij.uiDesigner.core.GridConstraints(5, 3, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_CENTER, com.intellij.uiDesigner.core.GridConstraints.FILL_NONE, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, null, null, 0, false));
        img = new JLabel();
        img.setText("");
        cvPanel.add(img, new com.intellij.uiDesigner.core.GridConstraints(10, 0, 1, 1, com.intellij.uiDesigner.core.GridConstraints.ANCHOR_WEST, com.intellij.uiDesigner.core.GridConstraints.FILL_NONE, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, com.intellij.uiDesigner.core.GridConstraints.SIZEPOLICY_FIXED, null, null, null, 0, false));
    }

    /**
     * @noinspection ALL
     */
    private Font $$$getFont$$$(String fontName, int style, int size, Font currentFont) {
        if (currentFont == null) return null;
        String resultName;
        if (fontName == null) {
            resultName = currentFont.getName();
        } else {
            Font testFont = new Font(fontName, Font.PLAIN, 10);
            if (testFont.canDisplay('a') && testFont.canDisplay('1')) {
                resultName = fontName;
            } else {
                resultName = currentFont.getName();
            }
        }
        Font font = new Font(resultName, style >= 0 ? style : currentFont.getStyle(), size >= 0 ? size : currentFont.getSize());
        boolean isMac = System.getProperty("os.name", "").toLowerCase(Locale.ENGLISH).startsWith("mac");
        Font fontWithFallback = isMac ? new Font(font.getFamily(), font.getStyle(), font.getSize()) : new StyleContext().getFont(font.getFamily(), font.getStyle(), font.getSize());
        return fontWithFallback instanceof FontUIResource ? fontWithFallback : new FontUIResource(fontWithFallback);
    }

    /**
     * @noinspection ALL
     */
    public JComponent $$$getRootComponent$$$() {
        return cvPanel;
    }
}
