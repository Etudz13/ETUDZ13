حول html الى https
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<     <thead>
      <tr>
        <th>المقياس</th>
        <th>المعامل</th>
        <th>الرصيد</th>
        <th>الوحدة</th>
        <th>تطبيق؟</th>
        <th>نقاط الامتحان</th>
        <th>نقاط التطبيق</th>
        <th>المعدل النهائي</th>
        <th>حذف</th>
      </tr>
    </thead>
    <tbody id="tableBody">
      <tr>
        <td>القانون المدني - أحكام الالتزامات</td>
        <td><input type="number" value="2" class="coeff"></td>
        <td>7</td>
        <td>أساسية</td>
        <td>
          <select class="has-practical"><option value="true">نعم</option><option value="false">لا</option></select>
        </td>
        <td><input type="number" min="0" max="20" class="exam" oninput="calculate()"></td>
        <td><input type="number" min="0" max="20" class="practical" oninput="calculate()"></td>
        <td class="highlight result">0.00</td>
        <td><button class="delete-button" onclick="this.closest('tr').remove(); calculate();">حذف</button></td>
      </tr>
      <tr>
        <td>قانون الإجراءات الجزائية</td>
        <td><input type="number" value="2" class="coeff"></td>
        <td>7</td>
        <td>أساسية</td>
        <td>
          <select class="has-practical"><option value="true">نعم</option><option value="false">لا</option></select>
        </td>
        <td><input type="number" min="0" max="20" class="exam" oninput="calculate()"></td>
        <td><input type="number" min="0" max="20" class="practical" oninput="calculate()"></td>
        <td class="highlight result">0.00</td>
        <td><button class="delete-button" onclick="this.closest('tr').remove(); calculate();">حذف</button></td>
      </tr>
      <tr>
        <td>قانون الإجراءات المدنية والإدارية</td>
        <td><input type="number" value="1" class="coeff"></td>
        <td>4</td>
        <td>أساسية</td>
        <td>
          <select class="has-practical"><option value="true">نعم</option><option value="false">لا</option></select>
        </td>
        <td><input type="number" min="0" max="20" class="exam" oninput="calculate()"></td>
        <td><input type="number" min="0" max="20" class="practical" oninput="calculate()"></td>
        <td class="highlight result">0.00</td>
        <td><button class="delete-button" onclick="this.closest('tr').remove(); calculate();">حذف</button></td>
      </tr>
      <tr>
        <td>منهجية العلوم القانونية</td>
        <td><input type="number" value="1" class="coeff"></td>
        <td>6</td>
        <td>منهجية</td>
        <td>
          <select class="has-practical"><option value="true">نعم</option><option value="false">لا</option></select>
        </td>
        <td><input type="number" min="0" max="20" class="exam" oninput="calculate()"></td>
        <td><input type="number" min="0" max="20" class="practical" oninput="calculate()"></td>
        <td class="highlight result">0.00</td>
        <td><button class="delete-button" onclick="this.closest('tr').remove(); calculate();">حذف</button></td>
      </tr>
      <tr>
        <td>قانون العمل</td>
        <td><input type="number" value="1" class="coeff"></td>
        <td>2</td>
        <td>استكشافية</td>
        <td>
          <select class="has-practical"><option value="false">لا</option><option value="true">نعم</option></select>
        </td>
        <td><input type="number" min="0" max="20" class="exam" oninput="calculate()"></td>
        <td><input type="number" min="0" max="20" class="practical" oninput="calculate()"></td>
        <td class="highlight result">0.00</td>
        <td><button class="delete-button" onclick="this.closest('tr').remove(); calculate();">حذف</button></td>
      </tr>
      <tr>
        <td>حقوق الإنسان</td>
        <td><input type="number" value="1" class="coeff"></td>
        <td>2</td>
        <td>استكشافية</td>
        <td>
          <select class="has-practical"><option value="false">لا</option><option value="true">نعم</option></select>
        </td>
        <td><input type="number" min="0" max="20" class="exam" oninput="calculate()"></td>
        <td><input type="number" min="0" max="20" class="practical" oninput="calculate()"></td>
        <td class="highlight result">0.00</td>
        <td><button class="delete-button" onclick="this.closest('tr').remove(); calculate();">حذف</button></td>
      </tr>
      <tr>
        <td>لغة أجنبية (مصطلحات قانونية)</td>
        <td><input type="number" value="1" class="coeff"></td>
        <td>2</td>
        <td>أفقية</td>
        <td>
          <select class="has-practical"><option value="false">لا</option><option value="true">نعم</option></select>
        </td>
        <td><input type="number" min="0" max="20" class="exam" oninput="calculate()"></td>
        <td><input type="number" min="0" max="20" class="practical" oninput="calculate()"></td>
        <td class="highlight result">0.00</td>
        <td><button class="delete-button" onclick="this.closest('tr').remove(); calculate();">حذف</button></td>
      </tr>
    </tbody>
  </table>

  <button class="add-button" onclick="addRow()">➕ إضافة مقياس</button>
  <button class="reset-button" onclick="resetAll()">🗑️ مسح جميع النتائج</button>

  <div class="final-grade">
    المعدل العام: <span class="highlight" id="overall">0.00</span>
  </div>

  <div class="mk13">MK13</div>

  <script>
    function calculate() {
      let total = 0;
      let totalCoeff = 0;
      const rows = document.querySelectorAll("#tableBody tr");

      rows.forEach(row => {
        const coeff = parseFloat(row.querySelector(".coeff")?.value) || 0;
        const exam = parseFloat(row.querySelector(".exam")?.value);
        const practical = parseFloat(row.querySelector(".practical")?.value);
        const hasPractical = row.querySelector(".has-practical")?.value === "true";

        let avg = 0;
        if (!isNaN(exam)) {
          avg = hasPractical && !isNaN(practical)
            ? exam * 0.6 + practical * 0.4
            : exam;
        }

        row.querySelector(".result").innerText = avg.toFixed(2);
        if (!isNaN(avg)) {
          total += avg * coeff;
          totalCoeff += coeff;
        }
      });

      const overall = totalCoeff > 0 ? (total / totalCoeff).toFixed(2) : "0.00";
      document.getElementById("overall").innerText = overall;
    }

    function addRow() {
      const tbody = document.getElementById("tableBody");
      const row = document.createElement("tr");

      row.innerHTML = `
        <td><input type="text" placeholder="اسم المقياس"></td>
        <td><input type="number" min="1" max="5" value="1" class="coeff"></td>
        <td><input type="number" min="1" max="10" value="1"></td>
        <td>
          <select>
            <option>أساسية</option>
            <option>استكشافية</option>
            <option>أفقية</option>
            <option>منهجية</option>
          </select>
        </td>
        <td>
          <select class="has-practical">
            <option value="true">نعم</option>
            <option value="false">لا</option>
          </select>
        </td>
        <td><input type="number" min="0" max="20" class="exam" oninput="calculate()"></td>
        <td><input type="number" min="0" max="20" class="practical" oninput="calculate()"></td>
        <td class="highlight result">0.00</td>
        <td><button class="delete-button" onclick="this.closest('tr').remove(); calculate();">حذف</button></td>
      `;
      tbody.appendChild(row);
    }

    function resetAll() {
      document.querySelectorAll("#tableBody input").forEach(input => input.value = "");
      document.querySelectorAll(".result").forEach(cell => cell.innerText = "0.00");
      document.getElementById("overall").innerText = "0.00";
    }
  </script>

</body>
</html>
  
