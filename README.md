

### Example of Using Gemini AI:

```javascript
import { GoogleGenerativeAI } from "@google/generative-ai";

const genAI = new GoogleGenerativeAI(process.env.VITE_GEMINI_API_KEY);

const readFileAsBase64 = (file) => {
  return new Promise((resolve, reject) => {
    const reader = new FileReader();
    reader.onload = () => resolve(reader.result.split(",")[1]);
    reader.onerror = reject;
    reader.readAsDataURL(file);
  });
};

const handleFileUpload = async (file, filetype) => {
  const base64Data = await readFileAsBase64(file);
  const imageParts = [
    {
      inlineData: {
        data: base64Data,
        mimeType: filetype,
      },
    },
  ];

  const model = genAI.getGenerativeModel({ model: "gemini-1.5-pro" });
  const prompt = "Analyze this medical image and provide insights.";

  const result = await model.generateContent([prompt, ...imageParts]);
  const response = await result.response;
  console.log(response.text());
};
```

## 🤝 Contributing

Contributions are welcome! Please fork the repository and submit a pull request for any improvements or bug fixes.

## 📜 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
