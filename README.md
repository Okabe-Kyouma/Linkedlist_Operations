# Linkedlist_Operations

// Online Java Compiler
// Use this editor to write, compile and run your Java code online
import java.util.*;
class Node<T>{
    
    T data;
    Node<T> next;
    
    public Node(T data,Node<T> next){
        this.data  = data;
        this.next = next;
    }
    
}

class HelloWorld {
    public static void main(String[] args) {
        
     Node<Integer> head = createLLIteratively();
     
     System.out.println("working");
    
          print(removeKNodesFromK(head,2,2));
     
       
    }
    
    public static Node<Integer> removeKNodesFromK(Node<Integer> head,int position,int n){
        
        Node<Integer> node = head;
        
        if(head==null){
            return head;
        }
        
        while(node!=null){
            
            position--;
           
            
            if(position<=0){
                
                Node<Integer> ans = node;
                while(ans!=null && n!=-1){
                    
                    
                    ans = ans.next;
                    n--;
                    
                }
                
                node.next = ans;
                return head;
                
                
            }
            
             node = node.next;
            
        }
        
        return null;
        
        
    }
    
    public static Node<Integer> oddThenEvenOrder(Node<Integer> head){
        
        if(head==null){
            return null;
        }
        
        Node<Integer> n = oddThenEvenOrder(head.next);
        
        if(n==null){
            return head;
        }
        else{
            
            if(head.data%2==0 && n.data%2!=0){
                head.next = null;
                Node<Integer> temp = head;
                Node<Integer> node = n;
                Node<Integer> sas = null;
                
                while(node.next!=null && node.next.data%2!=0){
                    node = node.next;
                }
                
                if(node.next!=null){
                    sas = node.next;
                }
                
                node.next = head;
                head.next = sas;
                return n;
                
                
                // n.next = tmep;
                // return n;
            }
            else{
                 head.next = n;
                 return head;
            }
            
            
            
        }
        
        
    }
    
    public static int findMidNodeValue(Node<Integer> head){
        
        if(head==null){
            return -1;
        }
        
        if(head.next==null){
            return head.data;
        }
        
        Node<Integer> slow = head;
        Node<Integer> fast = head.next;
        
        while(fast!=null && fast.next!=null){
            
            slow = slow.next;
            fast = fast.next;
            fast = fast.next;
            
        }
        
        return slow.data;
        
        
    }
    
    public static int firstOcc(Node<Integer> head,int n,int count){
        
        if(head==null){
            return -1;
        }
        
        if(head.data==n){
            return count;
        }
        
    return firstOcc(head.next,n,++count);
        
        
    }
    
    public static Node<Integer> mergeTwoSortedLinkedList(Node<Integer> list1,Node<Integer> list2){
        
        if(list1==null){
            return list2;
        }
        if(list2==null){
            return list1;
        }
        
        Node<Integer> first = list1;
        Node<Integer> second = list2;
        Node<Integer> arr = new Node(0,null);
        
        while(first!=null && second!=null){
            
            int firstValue = first.data;
            int secondValue = second.data;
            
            if(firstValue>secondValue){
                arr = insertAtLast(arr,secondValue);
                second = second.next;
            }
            else{
                arr = insertAtLast(arr,firstValue);
                first = first.next;
            }
            
            
        }
        
        while(first!=null){
            
            int value = first.data;
            
            arr = insertAtLast(arr,value);
            
            first = first.next;
        }
        
        while(second!=null){
            
            int value = second.data;
            arr = insertAtLast(arr,value);
            second = second.next;
            
        }
        
        
        return arr.next;
        
        
    }
    
    public static Node<Integer> deleteAtMidRecursively(Node<Integer> head,int position){
        
        
        if(head==null){
            return head;
        }
        
        if(position==0){
            return head.next;
        }
        
        Node<Integer> n = deleteAtMidRecursively(head.next,--position);
        
         head.next = n;
         return head;
        
        
    }
    
    public static Node<Integer> insertAtMidRecursively(Node<Integer> head,int value,int position){
        
        if(head==null && position==0){
            Node<Integer> node = new Node(value,null);
            return node;
        }
        
        if(head==null){
            return null;
        }
        
        if(position==0){
          Node<Integer> temp = head;
          Node<Integer> node = new Node(value,null);
          node.next = temp;
          return node;
        }
        
       Node<Integer> val =  insertAtMidRecursively(head.next,value,--position);
        
        head.next = val;
        
        return head;
        
    }
    
    public static Node<Integer> lListCreationRecursively(){
        
        
        Scanner input = new Scanner(System.in);
        
        int data = input.nextInt();
        
        if(data==-1){
            return null;
        }
        
        Node<Integer> temp = new Node(data,null);
        
        Node<Integer> n = lListCreationRecursively();
        
        if(n==null){
            return temp;
        }
        else{
            temp.next = n;
            return temp;
        }
        
        
        
    }
    
    public static Node<Integer> createLLIteratively(){
        
         Scanner input = new Scanner(System.in);
        
        int data = input.nextInt();
        
        Node<Integer> n = null;
        
        while(data!=-1){
            
            if(n==null)
           n = new Node(data,null);
            else{
               n = insertAtLast(n,data);
            }
            data = input.nextInt();       
        }
        
        return n;
        
    }
    
    //public static Node<Integer> directCreationOfLL(){
        
          //   Node<Integer> head = new Node(10,null);
    //   head = insertAtLast(head,20);
    //   head = insertAtFirst(head,0);
    //   head = insertAtMid(head,50,3);
    // return head;
        
        
    //}
    
    public static void printReverseList(Node<Integer> head){
        
        if(head==null){
            return;
        }
        
        printReverseList(head.next);
        
        System.out.println(head.data);
        
        
    }
    
    public static boolean isPalindrome(Node<Integer> head){
        
        if(head==null){
            return true;
        }
        
        
         Node<Integer> newLL = null;
    
         newLL = copyLL(head);
        
        newLL = reverseRecursion(newLL);
        
          while(head!=null){
              
              if(newLL.data!=head.data){
                  return false;
              }
              
              newLL = newLL.next;
              head = head.next;
              
          }
        
        
        return true;
        
        
        
    }
    
    public static Node<Integer> copyLL(Node<Integer> original){
        
        if(original==null){
            return original;
        }
        
        Node<Integer> newLL = new Node(0,null);
        
        while(original!=null){
            
            int value = original.data;
            // int next = original.next;
            
            newLL = insertAtLast(newLL,value);
            
         original = original.next;
            
        }
        
        return newLL.next;
        
        
    }
    
    public static Node<Integer> reverseRecursion(Node<Integer> head){
        
        if(head==null){
            return head;
        }
        
        Node n = reverseRecursion(head.next);
        
        if(n==null){
            return head;
        }
        else{
            int value = head.data;
            n = insertAtLast(n,value);
            return n;
        }
        
        
    }
    
    public static Node<Integer> removeConsecutiveDuplicate(Node<Integer> head){
        
        if(head==null || head.next==null){
            return head;
        }
        
        Node<Integer> slow = head;
        
        Node<Integer> fast = head.next;
        
        boolean flag;
        
        while(fast!=null){
            flag = false;
            while(fast!=null && slow.data==fast.data){
                
                if(!flag)
                slow.next = null;
                
                flag = true;
                
                fast = fast.next;
            }
            
            if(flag){
                slow.next = fast;
            }
            
            if(fast==null){
                break;
            }
            
            slow = slow.next;
            fast = fast.next;
            
            
        }
        
        return head;
        
    }
    
    
    public static Node<Integer> append(Node<Integer> head,int posi){
        
        if(head==null){
            return head;
        }
        
        posi--;
        
        Node<Integer> temp = head;
        
        while(posi!=0 && temp!=null){
            posi--;
            temp = temp.next;
        }
        
        Node<Integer> start = temp.next;
        temp.next = null;
        Node<Integer> starts = start;
        
        while(starts.next!=null){
            starts = starts.next;
        }
        
        starts.next = head;
        
        return start;
        
        
        
        
        
        
        
        
    }
    
    public static Node<Integer> insertAtMid(Node<Integer> head,int value,int position){
        
        Node<Integer> add = new Node(value,null);
        
        position--;
        
        Node<Integer> temp = head;
        
        while(position!=0 && temp!=null){
            position--;
            temp = temp.next;
        }
        
        Node<Integer> n = temp.next;
        
        temp.next = add;
        
        add.next = n;
        
        return head;
        
        
    }
    
    public static Node<Integer> insertAtLast(Node<Integer> head,int value){
        
        if(head==null){
            return null;
        }
        
        Node<Integer> n = new Node(value,null);
        
        Node<Integer> temp = head;
        
        while(temp.next!=null){
            temp = temp.next;
        }
        
        temp.next = n;
        
        return head;
        
        
    }
    
    public static Node<Integer> increnmentValuesByOne(Node<Integer> head){
        
        Node<Integer> temp = head;
        
        while(temp!=null){
            temp.data++;
            temp = temp.next;
        }
        
        return head;
    }
    
    public static void printIndexData(Node<Integer> head,int index){
        
        Node<Integer> temp = head;
        
        while(index!=0 && temp!=null){
            index--;
            temp = temp.next;
        }
        
        if(temp!=null)
        System.out.println(temp.data);
        
    }
    
    public static int length(Node<Integer> head){
        
        Node<Integer> n = head;
        int count  =0;
        
        while(n!=null){
            count++;
            n = n.next;
        }
        
        return count;
        
    }
    
    public static Node<Integer> insertAtFirst(Node<Integer> head,int value){
        
        if(head==null){
            return null;
        }
        
        Node<Integer> n = new Node(value,head);
        
        return n;
        
        
    }
    
   
    
    public static void print(Node<Integer> head){
        
        Node<Integer> temp = head;
        
        while(temp!=null){
            System.out.println(temp.data);
            temp = temp.next;
        }
        
    }
    
    
}

