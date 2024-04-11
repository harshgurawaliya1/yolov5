# yolov5
![Screenshot 2024-04-11 at 5 02 06 AM](https://github.com/harshgurawaliya1/yolov5/assets/106898396/57e5ed67-a107-46e1-baba-20eb680024d6)
class AutoShape(nn.Module):
    def __init__(self):
        super(AutoShape, self).__init__()
        self.model = DetectMultiBackend(
            model=Model(
                model=nn.Sequential(
                    Conv(
                        conv=nn.Conv2d(3, 32, kernel_size=(6, 6), stride=(2, 2), padding=(2, 2)),
                        act=nn.SiLU(inplace=True)
                    ),
                    Conv(
                        conv=nn.Conv2d(32, 64, kernel_size=(3, 3), stride=(2, 2), padding=(1, 1)),
                        act=nn.SiLU(inplace=True)
                    ),
                    C3(
                        cv1=Conv(
                            conv=nn.Conv2d(64, 32, kernel_size=(1, 1), stride=(1, 1)),
                            act=nn.SiLU(inplace=True)
                        ),
                        cv2=Conv(
                            conv=nn.Conv2d(64, 32, kernel_size=(1, 1), stride=(1, 1)),
                            act=nn.SiLU(inplace=True)
                        ),
                        cv3=Conv(
                            conv=nn.Conv2d(64, 64, kernel_size=(1, 1), stride=(1, 1)),
                            act=nn.SiLU(inplace=True)
                        ),
                        m=nn.Sequential(
                            Bottleneck(
                                cv1=Conv(
                                    conv=nn.Conv2d(32, 32, kernel_size=(1, 1), stride=(1, 1)),
                                    act=nn.SiLU(inplace=True)
                                ),
                                cv2=Conv(
                                    conv=nn.Conv2d(32, 32, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1)),
                                    act=nn.SiLU(inplace=True)
                                )
                            )
                        )
                    ),
                    Conv(
                        conv=nn.Conv2d(64, 128, kernel_size=(3, 3), stride=(2, 2), padding=(1, 1)),
                        act=nn.SiLU(inplace=True)
                    ),
                    # Continue defining the layers...
                )
            )
        )
        
    def forward(self, x):
        return self.model(x)
