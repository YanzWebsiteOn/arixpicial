const axios = require('axios');

module.exports = function(app) {
  // API Key yang valid
  const ApikeyReal = "rafael"; // API key yang harus digunakan

  // Fungsi untuk membuat pembayaran
  async function createPayment(apikey, amount, codeqr) {
    try {
      // Periksa apakah API key yang diberikan valid
      if (apikey !== ApikeyReal) {
        return { error: 'API key tidak valid.' };
      }

      // API key untuk API eksternal yang berbeda
      const apiKeyExternal = "rafael"; // Sesuaikan API key untuk API eksternal
      const url = `https://rafaelxd.tech/api/orkut/createpayment?apikey=${apiKeyExternal}&amount=${amount}&codeqr=${codeqr}`;

      // Melakukan permintaan ke API eksternal dengan API key yang benar
      const response = await axios.get(url);

      if (response.data.status) {
        return response.data;
      } else {
        throw new Error('API Error: Response status is false');
      }
    } catch (error) {
      console.error('Error:', error.message);
      return { error: 'Terjadi kesalahan saat memproses permintaan.' };
    }
  }

  // Endpoint '/createpayment'
  app.get('/createpayment', async (req, res) => {
    try {
      const { apikey, amount, codeqr } = req.query;

      // Periksa apakah parameter apikey, amount, dan codeqr ada
      if (!apikey || !amount || !codeqr) {
        return res.status(400).json({ error: 'Parameter "apikey", "amount", dan "codeqr" wajib disediakan.' });
      }

      // Panggil fungsi untuk membuat pembayaran jika API key valid
      const response = await createPayment(apikey, amount, codeqr);

      // Jika ada error dalam response
      if (response.error) {
        return res.status(401).json({ error: response.error });
      }

      // Jika API key valid, kembalikan respons yang sukses
      res.status(200).json({
        status: 200,
        creator: "ArixOffc",
        data: response
      });
    } catch (error) {
      res.status(500).json({ error: error.message });
    }
  });
};
