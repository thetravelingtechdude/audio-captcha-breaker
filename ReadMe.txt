Step 1: Create the training dataset

python audioGenerate.py --length 4 --count 2000 --output-dir training-audio --symbols symbols.txt


Step 2: Create the validation dataset

python audioGenerate.py --length 4 --count 400 --output-dir validation-audio --symbols symbols.txt


Step 3: Convert training dataset to images

python audioImageConverter.py --src-dir training-audio --dest-dir training-audio2images --n 4


Step 4: Convert validation dataset to images

python audioImageConverter.py --src-dir validation-audio --dest-dir validation-audio2images --n 4



Step 5: Train the model

python train.py --width 128 --height 64 --length 4 --symbols symbols.txt --batch-size 4 --epochs 2 --output-model SampleAudioModel.h5 --train-dataset training-audio2images --validate-dataset validation-audio2images

Step 6: Create a test dataset

python audioGenerate.py --length 4 --count 200 --output-dir testing-audio --symbols symbols.txt


Step 7: Convert test dataset to images

python audioImageConverter.py --src-dir testing-audio --dest-dir testing-audio2images --n 4


Step 8: Make classifications

audioClassify.py --model-name SampleAudioModel.h5 --captcha-dir test-dataset --output output.txt --symbols symbols.txt 

