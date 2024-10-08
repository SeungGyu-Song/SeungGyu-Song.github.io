Bag은 용량을 위해 compressed Image로 저장한다. 

근데 실제 코드 돌릴 때는 ros1 launch file에서 
`<node name="republish_fl" type="republish" pkg="image_transport" output="screen" args="compressed [in:=/camera1/color/image_raw](in:=/camera1/color/image_raw) raw [out:=/cam0/image_raw](out:=/cam0/image_raw) _image_[transport:=compressed](transport:=compressed)"/>`

넣어주면 별도로 source code에서 고칠 필요 없이 바로 사용할 수 있다.