const express = require('express');
const bodyParser = require('body-parser');

const app = express();
app.use(bodyParser.json());

app.post('/bfhl', (req, res) => {
  const { array } = req.body;

  if (!Array.isArray(array)) {
    return res.status(400).json({
      is_success: false,
      error: 'Invalid input. Expected an array.'
    });
  }

  const evenNumbers = array.filter(num => num % 2 === 0);
  const oddNumbers = array.filter(num => num % 2 !== 0);
  const alphabets = array.filter(char => typeof char === 'string' && /^[a-zA-Z]$/.test(char));

  const userId = `${req.body.full_name}_${req.body.dob.replace(/-/g, '').slice(0, 8)}`;
  const emailId = `${userId}@example.com`;
  const rollNumber = '123456';

  res.status(200).json({
    is_success: true,
    user_id: userId,
    email_id: emailId,
    roll_number: rollNumber,
    even_numbers: evenNumbers,
    odd_numbers: oddNumbers,
    alphabets: alphabets.map(char => char.toUpperCase())
  });
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
