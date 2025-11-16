> [!important]
> 
> ### 특징
> 
> 1. `PhotosUI` 라이브러리 import
> 2. `.onChange` 를 통해서 행동 설정
> 3. 이미지 데이터 다룰때 UiKit 요소 사용 됨

  

```Swift
import PhotosUI

struct NewPostView: View {
    @State var caption = ""
    @State var selectedItem: PhotosPickerItem?
    @Binding var tabIndex: Int
    @State var postImage: Image?
    
    func convertImage(item: PhotosPickerItem?) async {
        guard let item = item else {return}
        guard let data = try? await item.loadTransferable(type: Data.self) else {return}
        guard let uiImage = UIImage(data: data) else {return}
        Image(uiImage: uiImage)
        self.postImage = Image(uiImage: uiImage)
    }
    
...
    
				PhotosPicker(selection: $selectedItem) {
                if let image = self.postImage {
		                // self.postImage 가 nil 이 아니면
                    image
                        .resizable()
                        .aspectRatio(contentMode: .fit)
                        .frame(maxWidth: .infinity)
                } else {
		                // self.postImage 가 nil 이면
                    Image(systemName: "photo.on.rectangle")
                        .resizable()
                        .aspectRatio(1, contentMode: .fit)
                        .frame(width: 100, height: 100)
                        .padding()
                        .tint(Color.black)
                }
                
            }
            .onChange(of: selectedItem) { oldValue, newValue in
                Task {
                    await convertImage(item: newValue)
                }
                
            }
```