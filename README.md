<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Trắc nghiệm Ma trận</title>

  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f3f6fb;
      margin: 0;
      padding: 30px;
    }

    .container {
      max-width: 850px;
      margin: auto;
      background: white;
      padding: 30px;
      border-radius: 18px;
      box-shadow: 0 8px 25px rgba(0,0,0,0.12);
    }

    h1 {
      text-align: center;
      color: #1f2937;
    }

    #score {
      font-weight: bold;
      color: #2563eb;
      margin-bottom: 20px;
    }

    .question {
      font-size: 21px;
      font-weight: bold;
      margin-bottom: 18px;
      color: #111827;
    }

    button.answer {
      display: block;
      width: 100%;
      text-align: left;
      margin: 10px 0;
      padding: 14px;
      border: none;
      border-radius: 12px;
      background: #e5e7eb;
      cursor: pointer;
      font-size: 16px;
    }

    button.answer:hover {
      background: #dbeafe;
    }

    .correct {
      background: #86efac !important;
    }

    .wrong {
      background: #fca5a5 !important;
    }

    #next {
      margin-top: 20px;
      padding: 13px 22px;
      border: none;
      border-radius: 12px;
      background: #2563eb;
      color: white;
      cursor: pointer;
      font-size: 16px;
      width: 100%;
    }

    #explain {
      margin-top: 15px;
      padding: 15px;
      background: #f9fafb;
      border-left: 5px solid #2563eb;
      border-radius: 8px;
      display: none;
    }
  </style>
</head>

<body>
  <div class="container">
    <h1>TRẮC NGHIỆM MA TRẬN</h1>
    <p id="score">Điểm hiện tại: 0/20</p>

    <div id="quiz"></div>
    <div id="explain"></div>

    <button id="next" onclick="nextQuestion()">Câu tiếp theo</button>
  </div>

  <script>
    const questions = [
      {
        question: "1. Ma trận là gì?",
        answers: [
          "Một số thực bất kỳ",
          "Một bảng gồm các phần tử được sắp xếp theo hàng và cột",
          "Một phương trình bậc hai",
          "Một tập hợp không có thứ tự"
        ],
        correct: 1,
        explain: "Ma trận là bảng chữ nhật gồm các phần tử được sắp xếp theo hàng và cột."
      },
      {
        question: "2. Ma trận vuông là ma trận có đặc điểm gì?",
        answers: [
          "Số hàng bằng số cột",
          "Chỉ có một hàng",
          "Chỉ có một cột",
          "Tất cả phần tử bằng 0"
        ],
        correct: 0,
        explain: "Ma trận vuông là ma trận có số hàng bằng số cột, ví dụ 2x2 hoặc 3x3."
      },
      {
        question: "3. Điều kiện để cộng hai ma trận là gì?",
        answers: [
          "Hai ma trận phải cùng cấp",
          "Hai ma trận phải đều là ma trận vuông",
          "Hai ma trận phải có định thức khác 0",
          "Hai ma trận phải có cùng đường chéo chính"
        ],
        correct: 0,
        explain: "Muốn cộng hai ma trận thì chúng phải có cùng số hàng và cùng số cột."
      },
      {
        question: "4. Ma trận không là ma trận như thế nào?",
        answers: [
          "Ma trận có toàn phần tử bằng 1",
          "Ma trận có toàn phần tử bằng 0",
          "Ma trận có định thức bằng 1",
          "Ma trận có số hàng bằng số cột"
        ],
        correct: 1,
        explain: "Ma trận không là ma trận mà tất cả phần tử đều bằng 0."
      },
      {
        question: "5. Ma trận đơn vị có đặc điểm gì?",
        answers: [
          "Đường chéo chính toàn số 1, các phần tử còn lại bằng 0",
          "Tất cả phần tử đều bằng 1",
          "Tất cả phần tử đều bằng 0",
          "Chỉ có một hàng"
        ],
        correct: 0,
        explain: "Ma trận đơn vị có vai trò giống số 1 trong phép nhân ma trận."
      },
      {
        question: "6. Ký hiệu thường dùng cho ma trận đơn vị là gì?",
        answers: [
          "O",
          "I",
          "A",
          "det(A)"
        ],
        correct: 1,
        explain: "Ma trận đơn vị thường được ký hiệu là I."
      },
      {
        question: "7. Định thức chỉ tính được cho loại ma trận nào?",
        answers: [
          "Ma trận hàng",
          "Ma trận cột",
          "Ma trận vuông",
          "Mọi loại ma trận"
        ],
        correct: 2,
        explain: "Định thức chỉ được xác định với ma trận vuông."
      },
      {
        question: "8. Nếu det(A) = 0 thì ma trận A như thế nào?",
        answers: [
          "Khả nghịch",
          "Không khả nghịch",
          "Là ma trận đơn vị",
          "Là ma trận đường chéo"
        ],
        correct: 1,
        explain: "Nếu định thức bằng 0 thì ma trận không có ma trận nghịch đảo."
      },
      {
        question: "9. Điều kiện để hai ma trận A và B nhân được với nhau là gì?",
        answers: [
          "Số hàng của A bằng số hàng của B",
          "Số cột của A bằng số hàng của B",
          "Số cột của A bằng số cột của B",
          "Hai ma trận phải cùng cấp"
        ],
        correct: 1,
        explain: "A nhân B được khi số cột của A bằng số hàng của B."
      },
      {
        question: "10. Nếu A có kích thước 2x3 và B có kích thước 3x4 thì AB có kích thước bao nhiêu?",
        answers: [
          "2x4",
          "3x3",
          "4x2",
          "2x3"
        ],
        correct: 0,
        explain: "Kích thước kết quả lấy số hàng của A và số cột của B, nên AB là 2x4."
      },
      {
        question: "11. Phép nhân ma trận có tính giao hoán không?",
        answers: [
          "Luôn có",
          "Không luôn luôn",
          "Chỉ có với ma trận 3x3",
          "Chỉ có với ma trận không"
        ],
        correct: 1,
        explain: "Thông thường AB khác BA, nên phép nhân ma trận không có tính giao hoán."
      },
      {
        question: "12. Ma trận chuyển vị của A được tạo bằng cách nào?",
        answers: [
          "Đổi hàng thành cột",
          "Đổi dấu tất cả phần tử",
          "Nhân tất cả phần tử với 0",
          "Chỉ giữ đường chéo chính"
        ],
        correct: 0,
        explain: "Ma trận chuyển vị được tạo bằng cách biến hàng thành cột và cột thành hàng."
      },
      {
        question: "13. Ký hiệu ma trận chuyển vị của A thường là gì?",
        answers: [
          "A⁻¹",
          "Aᵀ",
          "det(A)",
          "|A|"
        ],
        correct: 1,
        explain: "Ma trận chuyển vị của A thường được ký hiệu là Aᵀ."
      },
      {
        question: "14. Ma trận nghịch đảo của A thường ký hiệu là gì?",
        answers: [
          "Aᵀ",
          "A²",
          "A⁻¹",
          "det(A)"
        ],
        correct: 2,
        explain: "Ma trận nghịch đảo của A được ký hiệu là A⁻¹."
      },
      {
        question: "15. Điều kiện để ma trận A có nghịch đảo là gì?",
        answers: [
          "A là ma trận vuông và det(A) khác 0",
          "A có toàn số 0",
          "A không cần là ma trận vuông",
          "A có số hàng lớn hơn số cột"
        ],
        correct: 0,
        explain: "Ma trận khả nghịch khi nó là ma trận vuông và có định thức khác 0."
      },
      {
        question: "16. Ma trận đường chéo là ma trận như thế nào?",
        answers: [
          "Chỉ các phần tử trên đường chéo chính có thể khác 0, còn lại bằng 0",
          "Tất cả phần tử đều khác 0",
          "Chỉ có một hàng",
          "Chỉ có một cột"
        ],
        correct: 0,
        explain: "Ma trận đường chéo có các phần tử ngoài đường chéo chính đều bằng 0."
      },
      {
        question: "17. Ma trận tam giác trên là ma trận có đặc điểm gì?",
        answers: [
          "Các phần tử phía dưới đường chéo chính bằng 0",
          "Các phần tử phía trên đường chéo chính bằng 0",
          "Tất cả phần tử bằng 0",
          "Tất cả phần tử bằng 1"
        ],
        correct: 0,
        explain: "Ma trận tam giác trên có các phần tử nằm dưới đường chéo chính bằng 0."
      },
      {
        question: "18. Ma trận tam giác dưới là ma trận có đặc điểm gì?",
        answers: [
          "Các phần tử phía trên đường chéo chính bằng 0",
          "Các phần tử phía dưới đường chéo chính bằng 0",
          "Đường chéo chính toàn số 0",
          "Không có đường chéo chính"
        ],
        correct: 0,
        explain: "Ma trận tam giác dưới có các phần tử nằm trên đường chéo chính bằng 0."
      },
      {
        question: "19. Hạng của ma trận thể hiện điều gì?",
        answers: [
          "Số hàng khác 0 độc lập tuyến tính lớn nhất",
          "Số phần tử trong ma trận",
          "Số cột của ma trận",
          "Tổng các phần tử trên đường chéo"
        ],
        correct: 0,
        explain: "Hạng ma trận cho biết số hàng hoặc cột độc lập tuyến tính lớn nhất."
      },
      {
        question: "20. Hệ phương trình tuyến tính có thể được biểu diễn bằng dạng ma trận nào?",
        answers: [
          "AX = B",
          "A + B = C",
          "AB = BA",
          "det(A) = 0"
        ],
        correct: 0,
        explain: "Hệ phương trình tuyến tính thường được viết dưới dạng AX = B."
      }
    ];

    let current = 0;
    let score = 0;
    let answered = false;

    function loadQuestion() {
      answered = false;
      const q = questions[current];

      document.getElementById("score").innerText =
        `Điểm hiện tại: ${score}/${questions.length}`;

      document.getElementById("explain").style.display = "none";
      document.getElementById("explain").innerHTML = "";

      let html = `<div class="question">${q.question}</div>`;

      q.answers.forEach((answer, index) => {
        html += `<button class="answer" onclick="checkAnswer(${index}, this)">
          ${String.fromCharCode(65 + index)}. ${answer}
        </button>`;
      });

      document.getElementById("quiz").innerHTML = html;
    }

    function checkAnswer(index, btn) {
      if (answered) return;
      answered = true;

      const q = questions[current];
      const buttons = document.querySelectorAll(".answer");

      if (index === q.correct) {
        btn.classList.add("correct");
        score++;
      } else {
        btn.classList.add("wrong");
        buttons[q.correct].classList.add("correct");
      }

      document.getElementById("score").innerText =
        `Điểm hiện tại: ${score}/${questions.length}`;

      const explainBox = document.getElementById("explain");
      explainBox.style.display = "block";
      explainBox.innerHTML = `<b>Giải thích:</b> ${q.explain}`;
    }

    function nextQuestion() {
      current++;

      if (current >= questions.length) {
        document.getElementById("quiz").innerHTML = `
          <h2>Hoàn thành bài trắc nghiệm!</h2>
          <p>Điểm cuối cùng của bạn là: <b>${score}/${questions.length}</b></p>
          <p>${score >= 16 ? "Quá ổn áp rồi 😭" : "Ôn lại phần ma trận thêm xíu là ngon nha 😭"}</p>
        `;

        document.getElementById("explain").style.display = "none";
        document.getElementById("next").style.display = "none";
        return;
      }

      loadQuestion();
    }

    loadQuestion();
  </script>
</body>
</html>
