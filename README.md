# ♻️ Waste Sorter

A browser-based waste classification app. Upload a photo or use your camera, and the app tells you what type of waste it is and which bin it belongs in.

The model was trained with [Google Teachable Machine](https://teachablemachine.withgoogle.com/) and runs entirely in the browser using TensorFlow.js. There is no backend server, so it is fast, free to host and works on phones.

**Live demo:** https://waste-sorter-web.vercel.app/

## Features

- Upload a photo or capture one with your camera
- Predicts the waste type with a confidence score for every class
- Shows a disposal tip for the predicted class
- Warns when the model is not sure (confidence below 60%)
- Works on desktop and mobile, with no installation

## Classes

The model recognises 9 classes:

`clothes`, `glass`, `cupboard`, `metal`, `paper`, `Plastic`, `carton`, `Battery`, `Trash`

## Tech stack

- [Google Teachable Machine](https://teachablemachine.withgoogle.com/) (Standard image model, 224x224 color images)
- [TensorFlow.js](https://www.tensorflow.org/js)
- [@teachablemachine/image](https://github.com/googlecreativelab/teachablemachine-community) helper library
- HTML, CSS and JavaScript (single page, no build step)
- Hosted on [Vercel](https://vercel.com/)

## Project structure

```
waste-sorter-web/
├── index.html          # the whole app (layout, styles, logic)
├── README.md
└── model/
    ├── model.json      # model architecture
    ├── metadata.json   # class labels and image size
    └── weights.bin     # trained weights
```

## Run locally

Browsers block loading the model from a file path, so use a small local server.

```bash
git clone https://github.com/<your-username>/waste-sorter-web.git
cd waste-sorter-web
python -m http.server 8000
```

Then open <http://localhost:8000>.

## Deploy to Vercel

1. Push this repo to GitHub.
2. On [vercel.com](https://vercel.com/), choose **Add New → Project** and import the repo.
3. Set **Framework Preset** to **Other** and leave the build command and output directory empty.
4. Click **Deploy**.

The camera needs HTTPS, which Vercel provides automatically.

## Retrain or update the model

1. Open Teachable Machine, add or fix images, and retrain.
2. Click **Export Model → Tensorflow.js → Download my model**.
3. Replace the three files in the `model/` folder with the new ones.
4. If you add or rename classes, update the `TIPS` list near the top of the script in `index.html`. The keys must match the class names in `metadata.json` (capital letters are ignored).
5. Commit and push. Vercel redeploys automatically.

## Limitations

- The model was trained on a limited set of images, so it can be wrong on unusual items, cluttered backgrounds or poor lighting. Photos on a plain background work best.
- It classifies one item per photo.
- The disposal tips are general guidance. Always follow your local waste collection rules.

## Dataset credits

_List the sources of your training images here, for example Kaggle Garbage Classification, TrashNet, Roboflow Universe datasets and your own campus photos, and check that each license allows your use._

## Author

Innocent Okiror, BSc. Computer Science, Mbarara University of Science and Technology (MUST), Uganda.

## License

_Choose a license (for example MIT) and add a `LICENSE` file, or remove this section._
