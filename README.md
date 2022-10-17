# Detect attack conversation & IP with supervised learning. Adversarial attack  

<https://github.com/miamor/Traffic-network-adversarial>  

Navigate to this [drive link](https://drive.google.com/drive/folders/1x4YxjIXItnTrDuSkzav0QXtJqC6heNvF?usp=sharing) to download all data, models and result.   


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
   