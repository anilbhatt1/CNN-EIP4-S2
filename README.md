# CNN-EIP4-S2
EIP4-S2 Files and assignment

Strategy Taken
--------------
1. Used 'use_bias = False' which helped to reduce the parameters.
2. Used filters of 10 to reduce the parameters in ultimate and pen-ultimate layers. 
Also since the receptive field was reduced to 6x6 and original size was only 28x28, there was no need to still maintain 16 channels in pen-ultimate layer. Hence reduced them to 10 filters and as expected, it didn't lead to any significant drop in accuracy.
3. Retained dropout value as 0.1 and kept it in all layers. Removing or altering values were not found to improve accuracy.
4. Retained BatchNormalization() in all layers as removing it in some layers was causing gap between train and validation accuracy to go up. Also, since the parameters where within 15K kept it to keep overfitting under control.
5. Batch size was retained as 128 as batch size of 32 was taking more time whereas batch size of 64 was not seen to give any added advantage.
6. Tried various 3x3 convolution combinations with varying filters like (a) 16-32-10x1-MP-then 10 all throughout (b) 16-32-10x1-MP-16-10x1-then 10 all throughout (c) 16-32-10x1-MP-16-16-10x1-then 10 all throughout. Also tried removing dropout from first layer and final 2 layers. But accuracy was seen plateuing at 0.9930-0.9936 range in all cases. Tried various combination of dropout values 0.25, 0.15, 0.05 etc. with the above listed filter combinations but mostly it was staying within 0.9930-0.9936 range. Hence used 3x3 convolution of 16-32-10x1-MP-16-16-16-10-10x4 with batchnormalization and dropout(0.1) at each layer.

Copy and paste the result of your model.evaluate (on test data)
---------------------------------------------------------------
score = model.evaluate(X_test, Y_test, verbose=0)
print(score)
[0.021625907252565958, 0.9943]

Copy and paste your Logs for 20 epochs
--------------------------------------

Train on 60000 samples, validate on 10000 samples
Epoch 1/20

Epoch 00001: LearningRateScheduler setting learning rate to 0.003.
60000/60000 [==============================] - 22s 368us/step - loss: 0.5280 - acc: 0.8586 - val_loss: 0.0912 - val_acc: 0.9792
Epoch 2/20

Epoch 00002: LearningRateScheduler setting learning rate to 0.0022744503.
60000/60000 [==============================] - 7s 109us/step - loss: 0.2516 - acc: 0.9325 - val_loss: 0.0585 - val_acc: 0.9855
Epoch 3/20

Epoch 00003: LearningRateScheduler setting learning rate to 0.0018315018.
60000/60000 [==============================] - 7s 109us/step - loss: 0.2006 - acc: 0.9406 - val_loss: 0.0499 - val_acc: 0.9867
Epoch 4/20

Epoch 00004: LearningRateScheduler setting learning rate to 0.0015329586.
60000/60000 [==============================] - 7s 109us/step - loss: 0.1718 - acc: 0.9458 - val_loss: 0.0377 - val_acc: 0.9901
Epoch 5/20

Epoch 00005: LearningRateScheduler setting learning rate to 0.0013181019.
60000/60000 [==============================] - 6s 107us/step - loss: 0.1545 - acc: 0.9479 - val_loss: 0.0440 - val_acc: 0.9856
Epoch 6/20

Epoch 00006: LearningRateScheduler setting learning rate to 0.0011560694.
60000/60000 [==============================] - 6s 107us/step - loss: 0.1419 - acc: 0.9488 - val_loss: 0.0311 - val_acc: 0.9918
Epoch 7/20

Epoch 00007: LearningRateScheduler setting learning rate to 0.0010295127.
60000/60000 [==============================] - 6s 108us/step - loss: 0.1335 - acc: 0.9503 - val_loss: 0.0347 - val_acc: 0.9903
Epoch 8/20

Epoch 00008: LearningRateScheduler setting learning rate to 0.0009279307.
60000/60000 [==============================] - 6s 107us/step - loss: 0.1275 - acc: 0.9516 - val_loss: 0.0300 - val_acc: 0.9926
Epoch 9/20

Epoch 00009: LearningRateScheduler setting learning rate to 0.0008445946.
60000/60000 [==============================] - 7s 109us/step - loss: 0.1245 - acc: 0.9508 - val_loss: 0.0278 - val_acc: 0.9924
Epoch 10/20

Epoch 00010: LearningRateScheduler setting learning rate to 0.0007749935.
60000/60000 [==============================] - 7s 111us/step - loss: 0.1160 - acc: 0.9542 - val_loss: 0.0294 - val_acc: 0.9920
Epoch 11/20

Epoch 00011: LearningRateScheduler setting learning rate to 0.0007159905.
60000/60000 [==============================] - 6s 107us/step - loss: 0.1111 - acc: 0.9550 - val_loss: 0.0247 - val_acc: 0.9928
Epoch 12/20

Epoch 00012: LearningRateScheduler setting learning rate to 0.000665336.
60000/60000 [==============================] - 6s 108us/step - loss: 0.1085 - acc: 0.9547 - val_loss: 0.0259 - val_acc: 0.9923
Epoch 13/20

Epoch 00013: LearningRateScheduler setting learning rate to 0.0006213753.
60000/60000 [==============================] - 7s 109us/step - loss: 0.1091 - acc: 0.9528 - val_loss: 0.0237 - val_acc: 0.9934
Epoch 14/20

Epoch 00014: LearningRateScheduler setting learning rate to 0.0005828638.
60000/60000 [==============================] - 7s 111us/step - loss: 0.1080 - acc: 0.9537 - val_loss: 0.0235 - val_acc: 0.9930
Epoch 15/20

Epoch 00015: LearningRateScheduler setting learning rate to 0.0005488474.
60000/60000 [==============================] - 6s 108us/step - loss: 0.0995 - acc: 0.9581 - val_loss: 0.0265 - val_acc: 0.9924
Epoch 16/20

Epoch 00016: LearningRateScheduler setting learning rate to 0.0005185825.
60000/60000 [==============================] - 7s 108us/step - loss: 0.1016 - acc: 0.9556 - val_loss: 0.0270 - val_acc: 0.9924
Epoch 17/20

Epoch 00017: LearningRateScheduler setting learning rate to 0.000491481.
60000/60000 [==============================] - 7s 109us/step - loss: 0.1005 - acc: 0.9568 - val_loss: 0.0224 - val_acc: 0.9935
Epoch 18/20

Epoch 00018: LearningRateScheduler setting learning rate to 0.0004670715.
60000/60000 [==============================] - 6s 108us/step - loss: 0.0962 - acc: 0.9584 - val_loss: 0.0221 - val_acc: 0.9939
Epoch 19/20

Epoch 00019: LearningRateScheduler setting learning rate to 0.0004449718.
60000/60000 [==============================] - 6s 107us/step - loss: 0.0981 - acc: 0.9562 - val_loss: 0.0206 - val_acc: 0.9933
Epoch 20/20

Epoch 00020: LearningRateScheduler setting learning rate to 0.000424869.
60000/60000 [==============================] - 6s 107us/step - loss: 0.0955 - acc: 0.9572 - val_loss: 0.0216 - val_acc: 0.9943
Out[64]:

