---
내용: 유저 검색 같은 키워드 검색기능을 스크롤뷰에 구현
유형: Modifier
---
```Swift
import SwiftUI
import Kingfisher

struct SearchView: View {
    @State var viewModel = SearchViewModel()
    @State var searchText = ""
    
    var filteredUsers: [User] {
        if searchText.isEmpty {
            return viewModel.users
        } else {
            return viewModel.users.filter { user in
                return user.username.lowercased().contains(searchText.lowercased())
            }
        }
    }
    
    var body: some View {
        
        NavigationStack {
            List {
                ForEach(filteredUsers) { user in
                    HStack {
                        NavigationLink {
                            ProfileView(viewModel: ProfileViewModel(user: user))
                        } label: {
                            if let imageUrl = user.profileImageUrl {
                                KFImage(URL(string: imageUrl))
                                    .resizable()
                                    .scaledToFit()
                                    .frame(width: 53, height: 53)
                                    .clipShape(Circle())
                            } else {
                                Image(systemName: "person.circle.fill")
                                    .resizable()
                                    .frame(width: 53, height: 53)
                                    .opacity(0.5)
                            }
                            
                            VStack (alignment: .leading) {
                                Text(user.username)
                                Text(user.bio ?? "")
                                    .foregroundStyle(.gray)
                            }
                        }

                        
                    }
                    .listRowSeparator(.hidden)
                }
            }
            .listStyle(.plain)
            .searchable(text: $searchText, prompt: "검색")
        }
    }
}
```