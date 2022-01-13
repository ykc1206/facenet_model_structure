## BasicConv2d
@startuml
map Conv {
    kernel_size => kernel_size
    stride => stride
}
map BN {
    eps => 0.001
    momentum => 0.1
    affine = True
}
map ReLU {
    
}
Conv-->BN
BN-->ReLU
@enduml
## Block35
@startuml
map Branch0 {
    BasicConv2d => (256, 32, kernel_size=1, stride=1)
}
map Branch1 {
    BasicConv2d_0 => (256, 32, kernel_size=1, stride=1)
    BasicConv2d_1 => (32, 32, kernel_size=3, stride=1, padding=1)
}
map Branch2 {
    BasicConv2d_0 => (256, 32, kernel_size=1, stride=1)
    BasicConv2d_1 => (32, 32, kernel_size=3, stride=1, padding=1)
    BasicConv2d_2 => (32, 32, kernel_size=3, stride=1, padding=1)
}
map Conv2d {
    in_channel => 96
    out_channel => 256
    kernel_size => 1
    stride =>1
}
map ReLU {
    
}
map Cat {

}
map Add {

}
map X {

}
X-->Branch0
X-->Branch1
X-->Branch2
X-->Add
Branch0-->Cat
Branch1-->Cat
Branch2-->Cat
Cat-->Conv2d
Conv2d-->Add
Add-->ReLU
@enduml
## Block17
@startuml
map Branch0 {
    BasicConv2d => (896, 128, kernel_size=1, stride=1)
}
map Branch1 {
    BasicConv2d_0 => (896, 128, kernel_size=1, stride=1)
    BasicConv2d_1 => (128, 128, kernel_size=(1, 7), stride=1, padding=(0, 3))
    BasicConv2d_2 => (128, 128, kernel_size=(7, 1), stride=1, padding=(3, 0))
}
map Conv2d {
    in_features => 256
    out_channel => 896
    kernel_size => 1
    stride => 1
}
map ReLU {
    
}
map X {

}
map Cat {

}
map Add {

}
X-->Branch0
X-->Branch1
X-->Add
Branch0-->Cat
Branch1-->Cat
Cat-->Conv2d
Conv2d-->Add
Add-->ReLU
@enduml
## Block8
@startuml
map Branch0 {
    BasicConv2d => (1792, 192, kernel_size=1, stride=1)
}
map Branch1 {
    BasicConv2d_0 => (1792, 192, kernel_size=1, stride=1)
    BasicConv2d_1 => (192, 192, kernel_size=(1, 3), stride=1, padding=(0, 1))
    BasicConv2d_2 => (192, 192, kernel_size=(3, 1), stride=1, padding=(1, 0))
}
map Conv2d {
    in_channel => 384
    out_channel => 1792
    kernel_size => 1
    stride => 1
}
map ReLU {
    
}
map X {

}
map Cat {

}
map Add {

}
X-->Branch0
X-->Branch1
Branch0-->Cat
Branch1-->Cat
Cat-->Conv2d
Conv2d-->Add
X-->Add
Add-->ReLU
@enduml
## Mixed_6a
@startuml
map Branch0 {
    BasicConv2d => (256, 384, kernel_size=3, stride=2)
}
map Branch1 {
    BasicConv2d_0 => (256, 192, kernel_size=1, stride=1)
    BasicConv2d_1 => (192, 192, kernel_size=3, stride=1, padding=1)
    BasicConv2d_2 => (192, 256, kernel_size=3, stride=2)
}
map Branch2 {
    MaxPool2d => (3, stride=2)
}
map X {

}
map Cat {

}
X-->Branch0
X-->Branch1
X-->Branch2
Branch0-->Cat
Branch1-->Cat
Branch2-->Cat
@enduml
## Mixed_7a
@startuml
map Branch0 {
    BasicConv2d_0 => (896, 256, kernel_size=1, stride=1)
    BasicConv2d_1 => (256, 384, kernel_size=3, stride=2)
}
map Branch1 {
    BasicConv2d_0 => (896, 256, kernel_size=1, stride=1)
    BasicConv2d_1 => (256, 256, kernel_size=3, stride=2)
}
map Branch2 {
    BasicConv2d => (896, 256, kernel_size=1, stride=1)
    BasicConv2d => (256, 256, kernel_size=3, stride=1, padding=1)
    BasicConv2d => (256, 256, kernel_size=3, stride=2)
}
map Branch3 {
    MaxPool2d => (3, stride)
}
map X {

}
map Cat {

}
X-->Branch0
X-->Branch1
X-->Branch2
X-->Branch3
Branch0-->Cat
Branch1-->Cat
Branch2-->Cat
Branch3-->Cat
@enduml
## InceptionResnetV1
@startuml
map Conv2d_1a {
    BasicConv2d => (3, 32, kernel_size=3, stride=2)
}
map Conv2d_2a {
    BasicConv2d => (32, 32, kernel_size=3, stride=1)
}
map Conv2d_2b {
    BasicConv2d => (32, 64, kernel_size=3, stride=1, padding=1)
}
map Maxpool_3a {
    MaxPool2d => (3, stride=2)
}
map Conv2d_3b {
    BasicConv2d => (64, 80, kernel_size=1, stride=1)
}
map Conv2d_4a {
    BasicConv2d => (64, 80, kernel_size=1, stride=1)
}
map Conv2d_4b {
    BasicConv2d => (192, 256, kernel_size=3, stride=2)
}
map Repeat_1 {
    Block35_0 => (scale=0.17)
    Block35_1 => (scale=0.17)
    Block35_2 => (scale=0.17)
    Block35_3 => (scale=0.17)
    Block35_4 => (scale=0.17)
}
map Mixed_6a {
    Mixed_6a
}
map Repeat_2 {
    Block17_0 => (scale=0.10)
    Block17_1 => (scale=0.10)
    Block17_2 => (scale=0.10)
    Block17_3 => (scale=0.10)
    Block17_4 => (scale=0.10)
    Block17_5 => (scale=0.10)
    Block17_6 => (scale=0.10)
    Block17_7 => (scale=0.10)
    Block17_8 => (scale=0.10)
    Block17_9 => (scale=0.10)
}
map Mixed_7a {
    Mixed_7a
}
map Repeat_3 {
    Block8_0 => (scale=0.20)
    Block8_1 => (scale=0.20)
    Block8_2 => (scale=0.20)
    Block8_3 => (scale=0.20)
    Block8_4 => (scale=0.20)
}
map Block8 {
    Block8 => (noReLU)
}
map Avgpool_1a {
    AdaptiveAvgPool2d => (1)
}
map Dropout {
    Dropout => (dropout_prob)
}
map FC {
    Linear => (1792, 512, bias=False)
}
map BN {
    BatchNorm1d => (512, eps=0.001, momentum=0.1, affine=True)
}
map Logits {
    Linear => (512, num_classes)
}
map X {

}
X-->Conv2d_1a
Conv2d_1a-->Conv2d_2a
Conv2d_2a-->Conv2d_2b
Conv2d_2b-->Maxpool_3a
Maxpool_3a-->Conv2d_3b
Conv2d_3b-->Conv2d_4a
Conv2d_4a-->Conv2d_4b
Conv2d_4b-->Repeat_1
Repeat_1-->Mixed_6a
Mixed_6a-->Repeat_2
Repeat_2-->Mixed_7a
Mixed_7a-->Repeat_3
Repeat_3-->Block8
Block8-->Avgpool_1a
Avgpool_1a-->Dropout
Dropout-->FC
FC-->BN
BN-->Logits
@enduml
