# ShoppingList
Bu proje, C# ve ASP.NET ile geliştirilmiş bir alışveriş listesi uygulamasıdır. SQL veritabanı bağlantısı kullanılarak kullanıcıların alışveriş listelerini yönetmelerine olanak tanır.

namespace WebApplication1
{
    public partial class WebForm3 : System.Web.UI.Page
    {
        string connectionString = @"Data Source=[YourDataSource];Initial Catalog=[YourProjectName];Integrated Security=True";
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void Button1_Click(object sender, EventArgs e)
        {
            string email = txt_giris_mail.Text.Trim();
            string password = txt_giris_sifre.Text;
            if (string.IsNullOrEmpty(email) || string.IsNullOrEmpty(password))
            {
                lblMessage.Text = "Lütfen tüm alanları doldurun.";
                lblMessage.Visible = true;
                return;
            }

            using (SqlConnection connection = new SqlConnection(connectionString))
            {
                connection.Open();

                string query = "SELECT COUNT(*) FROM kayit WHERE kullanici_mail = @Email AND kullanici_sifre = @Sifre";
                SqlCommand command = new SqlCommand(query, connection);
                command.Parameters.AddWithValue("@Email", email);
                command.Parameters.AddWithValue("@Sifre", password);

                int userCount = (int)command.ExecuteScalar();

                if (userCount > 0)
                {
                    // Giriş başarılı, kullanıcıyı ana sayfaya yönlendir
                    Session["UserEmail"] = email;
                    Response.Redirect("ShoppingList.aspx");
                }
                else
                {
                    lblMessage.Text = "Geçersiz e-posta veya şifre!";
                    lblMessage.Visible = true;
                }

                connection.Close();
            }

           
        }

        protected void Button2_Click(object sender, EventArgs e)
        {
            Response.Redirect("NewUser.aspx");
        }

        protected void Button3_Click(object sender, EventArgs e)
        {
            Response.Redirect("DeleteUser.aspx");
        }
    }
}
