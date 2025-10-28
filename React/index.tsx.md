#파일구조 

# 개요
- 폴더를 탐색할 때 가장 먼저 탐색되는 진입점 역할
- 폴더에 여러 컴포넌트가 있을경우 폴더의 index 파일만 훑어서 바로 컴포넌트를 import 할 수도 있음

# 사용법
## 컴포넌트 일괄 import

**❌ index.tsx가 없을 때**

``` ts
import { TaskList } from "~/app/dashboard/[teamId]/tasks/_components/TaskList/TaskList";
import { TaskItem } from "~/app/dashboard/[teamId]/tasks/_components/TaskList/TaskItem";
```

**✅ index.tsx가 있을 때**

``` ts
import { TaskList, TaskItem } from "~/app/dashboard/[teamId]/tasks/_components/TaskList";
```

