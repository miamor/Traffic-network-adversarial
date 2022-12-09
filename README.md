# Detect attack conversation & IP with supervised learning. Adversarial attack  

<https://github.com/miamor/Traffic-network-adversarial>  

Navigate to this [drive link](https://drive.google.com/drive/folders/18A4jHpMKlQZllyK2V4Ds9pufWk5WF8uG?usp=sharing) to download all data, models and result.   

## Result
### Original result of model output on test set
| 	precision |	recall |	f1-score |	Score |
--- | --- | --- | --- |
| Class 0 (normal) |	1.0000 |	0.9479 |	0.9732 |	18166 |
| Class 1 (attack) |	0.0596 |	1.0000 |	0.1125 |	60 |
| Accuracy |	 |		0.9480 |	18226 |
| Macro avg |	0.5298 |	0.9739 |	0.5429 |	18226 |
| Weighted avg |	0.9969 |	0.9480 |	0.9704 |	18226 |
| AUC |	 |	 | 	0.9739 |
### New result on test set after applying scoring threshold
| 	precision |	recall |	f1-score |	Score |
--- | --- | --- | --- |
| Class 0 (normal) |	1.0000 |	0.9620 |	0.9806 |	18166
| Class 1 (attack) |	0.0799 |	1.0000 |	0.1480 |	60
| Accuracy |	 |	 |	0.9621 |	18226
| Macro avg |	0.5399 |	0.9810 |	0.5643 |	18226
| Weighted avg |	0.9970 |	0.9621 |	0.9779 |	18226
| AUC |	 |	 |	 0.9810

### More on `Report.docx` and `u4-5.lr.ipynb`, `u4-6.evaluate.ipynb`, and `u4-7.adversarial.ipynb`.


## Folder description
`u0` : Generate features  
`u1` : Generate features for flows  
`u4-1` : Aggregate flows of the same `Conversation` (`SrcAddr->DstAddr`), `State`, and `Proto` within a window time (`window_width=7200(s)`, `window_stride=3600(s)`) into one record  
`u4-3` : Encode features of aggregated records  
`u4-5` : Run `logistic regression` model on encoded aggregated records  
`u4-6` : Evaluate model. Set threshold. Analysis detected result and select sample for next demonstration  
`u4-7` : Generate adversarial samples. Reproduce attack flows to bypass model  
`u4-8` : Pass new attack flows to the detection pipeline (`u1 -> u4-1 -> u4-3 -> u4-5`) to test the model performance on new attack flows.  

---

## Raw values for attack flows that can bypass the model.
`result/dfo_new1.csv` : Add 2 flows (minimum flows need to be inserted to fool the model).   
`result/dfo_new.csv` : Add 5 flows (more flows are added to reduce value of `BytesPerSec`). Reduce from `24906.267209` to `14750.948178` (we need at least one flow having `BytesPerSec = 14750.948178`)   
   