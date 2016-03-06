# IDontKnowWhatImDoing


Hi!
My nickname is Retrok and I am Programmer. I am programming C#! :D
Example: 

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.IO;

namespace LEL
{
    public partial class OknoProgramu : Form
    {
        List<string> jmena = new List<string>();
        List<string> prijmeni = new List<string>();
        List<int> vek = new List<int>();
        string path = "";

        public OknoProgramu()
        {
            InitializeComponent();
        }

        private void Btn_Load_Click(object sender, EventArgs e) //Spatne pojmenovana metoda - tohle je na ukladani predmetu
        {
            if (TB_Jmeno.Text != "" && TB_Prijmeni.Text != "" && TB_Vek.Text != "")
            {
                int vekHrace;
                if (int.TryParse(TB_Vek.Text, out vekHrace))
                {
                    jmena.Add(TB_Jmeno.Text);
                    prijmeni.Add(TB_Prijmeni.Text);

                    vek.Add(vekHrace);
                    MessageBox.Show(vekHrace.ToString());
                }
                else
                {
                    MessageBox.Show("V textboxu pro věk musí být jenom číslo");
                }


            }
            else
            {
                MessageBox.Show("Nevyplnil jsi všechny textboxy");
            }
            TB_Jmeno.Clear();
            TB_Prijmeni.Clear();
            TB_Vek.Clear();
        }

        private void Btn_Ulozit_Click(object sender, EventArgs e)
        {
            if (saveFileDialog1.ShowDialog() == DialogResult.OK)
            {
                path = saveFileDialog1.FileName;
            }
            using (StreamWriter soubor = new StreamWriter(path, false, Encoding.Default))
            {
                soubor.WriteLine("Jména;Příjmení;Věk");
                for (int i = 0; i < jmena.Count; i++)
                {
                    soubor.WriteLine("{0};{1};{2}", jmena[i], prijmeni[i], vek[i].ToString());
                }
            }
        }
    }
}
