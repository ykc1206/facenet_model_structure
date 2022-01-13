## PNet
@startuml
map Conv1 {
    in_channel => 3
    out_channel => 10
    kernel_size => 3
}
map PReLU1 {
    input_size => 10
}
map Pool1 {
    kernel_size => 2
    stride => 2
    ceil_mode => True
}
map Conv2 {
    in_channel =>10
    out_channel => 16
    kernel_size => 3
}
map PReLU2 {
    input_size => 16
}
map Conv3 {
    in_channel => 16
    out_channel => 32
    kernel_size => 3
}
map PReLU3 {
    input_size => 32
}
map Conv4_1 {
    in_channel => 32
    out_channel => 2
    kernel_size => 1
}
map Conv4_2 {
    in_channel => 32
    out_channel => 4
    kernel_size => 1
}
map Softmax4_1 {
    dim => 4
}

Conv1-->PReLU1
PReLU1-->Pool1
Pool1-->Conv2
Conv2-->PReLU2
PReLU2-->Conv3
Conv3-->PReLU3
PReLU3-->Conv4_1
Conv4_1-->Softmax4_1
PReLU3-->Conv4_2

@enduml
## RNet
@startuml
map Conv1 {
    in_channel => 3
    out_channel => 28
    kernel_size => 3
}
map PReLU1 {
    input_size => 28
}
map Pool1 {
    kernel_size => 3
    stride => 2
}
map Conv2 {
    in_channel => 28
    out_channel => 48
    kernel_size => 3
}
map PReLU2 {
    input_size => 48
}
map Pool2 {
    kernel_size => 3
    stride => 2
    ceil_mode => True
}
map Conv3 {
    in_channel => 48
    out_channel => 64
    kernel_size =>2
}
map PReLU3 {
    input_size =>64
}
map FC4 {
    in_features => 576
    out_featurs => 128
}
map PReLU4 {
    input_size => 128
}
map FC5_1 {
    in_features => 128
    out_featurs => 2
}
map Softmax5_1 {
    dim => 1
}
map FC5_2 {
    in_features => 128
    out_featurs =>4
}
map Permute {
    shape => (0, 3, 2, 1)
}
map Flatten {

}
Conv1-->PReLU1
PReLU1-->Pool1
Pool1-->Conv2
Conv2-->PReLU2
PReLU2-->Pool2
Pool2-->Conv3
Conv3-->PReLU3
PReLU3-->Permute
Permute-->Flatten
Flatten-->FC4
FC4-->PReLU4
PReLU4-->FC5_1
FC5_1-->Softmax5_1
PReLU4-->FC5_2
@enduml
## ONet
@startuml
map Conv1 {
    in_channel => 3
    out_channel => 32
    kernel_size =>3
}
map PReLU1 {
    input_size => 32
}
map Pool1 {
    kernel_size => 3
    stride => 2
    ceil_mode => True
}
map Conv2 {
    in_channel => 32
    out_channel => 64
    kernel_size => 3
}
map PReLU2 {
    input_size => 64
}
map Pool2 {
    kernel_size => 3
    stride => 2
    ceil_mode => True
}
map Conv3 {
    in_channel => 64
    out_channel => 64
    kernel_size =>3
}
map PReLU3 {
    input_size => 64
}
map Pool3 {
    kernel_size => 2
    stride => 2
}
map Conv4 {
    in_chanel => 64
    out_channel => 128
    kernel_size = 2
}
map PReLU4 {
    input_size => 128
}
map FC5 {
    in_features => 1152
    out_features => 256
}
map PReLU5 {
    input_size => 256
}
map FC6_1 {
    in_features => 256
    out_feature => 2
}
map Softmax6_1 {
    dim => 1
}
map FC6_2 {
    in_features => 256
    out_features => 4
}
map FC6_3 {
    in_features => 256
    out_features => 10
}
map Permute {
    shape => (0, 3, 2, 1)
}
map Flatten {

}
Conv1-->PReLU1
PReLU1-->Pool1
Pool1-->Conv2
Conv2-->PReLU2
PReLU2-->Pool2
Pool2-->Conv3
Conv3-->PReLU3
PReLU3-->Pool3
Pool3-->Conv4
Conv4-->PReLU4
PReLU4-->Permute
Permute-->Flatten
Flatten-->FC5
FC5-->PReLU5
PReLU5-->FC6_1
FC6_1-->Softmax6_1
PReLU5-->FC6_2
PReLU5-->FC6_3
@enduml
