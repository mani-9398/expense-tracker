const form = document.getElementById('transaction-form');
const transactionList = document.getElementById('transaction-list');
const incomeEl = document.getElementById('income');
const expenseEl = document.getElementById('expense');
const balanceEl = document.getElementById('balance');
const searchInput = document.getElementById('search');
const toggleBtn = document.getElementById('toggle-theme');
const exportBtn = document.getElementById('export');

let transactions = JSON.parse(localStorage.getItem('transactions')) || [];

function updateLocalStorage() {
  localStorage.setItem('transactions', JSON.stringify(transactions));
}

function updateSummary() {
  const income = transactions
    .filter(t => t.amount > 0)
    .reduce((acc, t) => acc + t.amount, 0);
  const expense = transactions
    .filter(t => t.amount < 0)
    .reduce((acc, t) => acc + Math.abs(t.amount), 0);

  incomeEl.textContent = income;
  expenseEl.textContent = expense;
  balanceEl.textContent = income - expense;
}

function renderTransactions(data = transactions) {
  transactionList.innerHTML = '';
  data.forEach(t => {
    const li = document.createElement('li');
    li.textContent = `${t.date} | ${t.category} | ${t.description} ₹${t.amount}`;
    transactionList.appendChild(li);
  });
}

form.addEventListener('submit', e => {
  e.preventDefault();

  const desc = document.getElementById('description').value;
  const amt = +document.getElementById('amount').value;
  const date = document.getElementById('date').value;
  const cat = document.getElementById('category').value;

  const newTrans = { description: desc, amount: amt, date, category: cat };
  transactions.push(newTrans);

  updateLocalStorage();
  updateSummary();
  renderTransactions();
  form.reset();
});

searchInput.addEventListener('input', () => {
  const keyword = searchInput.value.toLowerCase();
  const filtered = transactions.filter(t =>
    t.description.toLowerCase().includes(keyword) ||
    t.category.toLowerCase().includes(keyword)
  );
  renderTransactions(filtered);
});

toggleBtn.addEventListener('click', () => {
  document.body.classList.toggle('dark-mode');
});

exportBtn.addEventListener('click', () => {
  let csv = "Date,Category,Description,Amount\n";
  transactions.forEach(t => {
    csv += `${t.date},${t.category},${t.description},${t.amount}\n`;
  });

  const blob = new Blob([csv], { type: 'text/csv' });
  const url = window.URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'transactions.csv';
  a.click();
  window.URL.revokeObjectURL(url);
});

updateSummary();
renderTransactions();
