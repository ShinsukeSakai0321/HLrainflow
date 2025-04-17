HLrainflow
# HLrainflow

A simple and efficient implementation of the Rainflow counting algorithm for fatigue analysis in Python.

# Author
Shinsuke Sakai   
Yokohama National University

## Features

- Rainflow cycle counting for fatigue analysis
- Lightweight and dependency-free
- Supports peak-valley sequences or raw time-series input
- Easy to test and extend

## Installation

You can install the package via pip:

```bash
pip install HLrainflow
```

## Usage
ASTM E1049-85(2017) Rainflow Counting Example   
Refer to [Astm e 1049 85 standard practice for cycle counting in fatigue analysis](https://www.slideshare.net/slideshow/astm-e-1049-85-standard-practice-for-cycle-counting-in-fatigue-analysis/42141102)
```python
from HLrainflow import rainflow
Sample1=[-2,1,-3,5,-1,3,-4,4,-2]
peak=Sample1
hl=rainflow.HL()
hl.SetPeak(peak)
halfR,halfM=hl.hloop()
print('half range=',halfR)
print('half mean=',halfM)  
```

## Example Output
half range= [4.0, 4.0, 3.0, 4.0, 8.0, 9.0, 8.0, 6.0]   
half mean= [1.0, 1.0, -0.5, -1.0, 1.0, 0.5, 0.0, 1.0]

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## methods
|method|arguments|return var.|contents|
|------|---------|-----------|--------|
|SetPeak|peak:list|none|Set the peak:list to self.Peak|
|demo_data|none|data:list|Generate sample wave data|
|SetWave|wave:list|none|Set the wave:list to self.Wave|
|Calc|none|none|After calculating the peak values from self.wave, perform rainflow counting and store the results in self.halfR and self.halfM.|
|GetRes|none|self.halfR,self.halfM|Get half range list and half range mean.|
|GetPeak|none|self.Peak|Get peak list|
|peak|y0,y1,y2|flag,time,value|Calculate peak value and time from y0,y1,y2|
|PeakCalc|none|none|Calculate self.Peak from self.Wave|
|hloop|none|res_r,res_m|Execute rainflow counting for self.Peak| 






## Other Examples
### -1- Execute rainflow counting for given peak values
```python
from HLrainflow import rainflow
Sample1=[2,-14,10,0,13,-9,11,-8,8,-9,15,-4,10,0,13,0]
peak=Sample1
hl=rainflow.HL()
hl.SetPeak(peak)
halfR,halfM=hl.hloop()
print('half range=',halfR)
print('half mean=',halfM)
#half range= [10.0, 10.0, 16.0, 16.0, 20.0, 20.0, 22.0, 22.0, 10.0, 10.0, 16.0, 29.0, 19.0, 17.0, 13.0]
#half mean= [5.0, 5.0, 0.0, 0.0, 1.0, 1.0, 2.0, 2.0, 5.0, 5.0, -6.0, 0.5, 5.5, 4.5, 6.5]
```

### -2- Execute rainflow counting for demo sample wave
```python
from HLrainflow import rainflow
hl=rainflow.HL()
wave=hl.demo_data()
hl.SetWave(wave)
hl.Calc()
halfR,halfM=hl.GetRes()
print('half range=',halfR)
print('half mean=',halfM) 
#half range= [0.021989285714285715, 0.021989285714285715, 0.01238185975609756, 0.01238185975609756, 0.08263670741023682, 0.04894241486068111, 0.018175837320574165]
#half mean= [-0.009969642857142856, -0.009969642857142856, 0.0049096798780487805, 0.0049096798780487805, 0.003540412528647823, -0.013306733746130032, 0.0020765550239234447]
```

### -3- Calculate peak values from deme sample wave
```python
from HLrainflow import rainflow
hl=rainflow.HL()
wave=hl.demo_data()
hl.SetWave(wave)
hl.PeakCalc()
peak=hl.GetPeak()
print('peak value=',peak)
#peak value= [0.04485876623376624, -0.03777794117647059, 0.001025, -0.020964285714285713, 0.01110060975609756, -0.00128125, 0.011164473684210526, -0.007011363636363637]
```

### -4- Calculate peak values from given peak values
```python
from HLrainflow import rainflow
Sample1=[0,2,1,4,-3,2.5,-4,3,-5,0]
peak=Sample1
hl=rainflow.HL()
hl.SetPeak(peak)
halfR,halfM=hl.hloop()
print('half range=',halfR)
print('half mean=',halfM)
#half range= [1.0, 1.0, 5.5, 5.5, 7.0, 7.0, 4.0, 9.0, 5.0]
#half mean= [1.5, 1.5, -0.25, -0.25, -0.5, -0.5, 2.0, -0.5, -2.5] 
```
