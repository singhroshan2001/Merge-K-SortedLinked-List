# Merge-K-SortedLinked-List.
import java.io.*;
import java.util.*;
public class Main {
    static class SinglyLinkedListNode {
        public int data;
        public SinglyLinkedListNode next;
        public SinglyLinkedListNode(){}
        public SinglyLinkedListNode(int nodeData) {
            this.data = nodeData;
            this.next = null;
        }
    }
    static class SinglyLinkedList {
        public SinglyLinkedListNode head;
        public SinglyLinkedListNode tail;
        public SinglyLinkedList() {
            this.head = null;
            this.tail = null;
        }
        public void insertNode(int nodeData) {
            SinglyLinkedListNode node = new SinglyLinkedListNode(nodeData);

            if (this.head == null) {
                this.head = node;
            } else {
                this.tail.next = node;
            }

            this.tail = node;
        }
    }
    static void printLinkedList(SinglyLinkedListNode head)
    {
        SinglyLinkedListNode temp=head;
        while(temp!=null)
        {
            System.out.print(temp.data+" ");
            temp=temp.next;
        }
        System.out.println();
    }

// Complete the mergeKLists() function below.

    /*
    For your reference:
    static class SinglyLinkedListNode {
        public int data;
        public SinglyLinkedListNode next;
        public SinglyLinkedListNode(){}
        public SinglyLinkedListNode(int nodeData) {
            this.data = nodeData;
            this.next = null;
        }
    }

    */
    static SinglyLinkedListNode merge(SinglyLinkedListNode x, SinglyLinkedListNode y)
    {
      SinglyLinkedListNode res=null;
      if(x==null)
        return y;
      if(y==null)
        return x;
      if(x.data<=y.data)
      {
        res=x;
        res.next=merge(x.next,y);
      }
      else
      {
        res=y;
        res.next=merge(x,y.next);
      }
      return res;
    }
    static SinglyLinkedListNode mergeKLists(SinglyLinkedListNode []headList) {
    int k=headList.length-1;
    while(k!=0)
    {
      int i=0, j=k;
      while(i<j)
      {
        headList[i]=merge(headList[i], headList[j]);
        i++;
        j--;
        if(i>=j)
          k=j;
      }
    }
    return headList[0];

    }


    private static final Scanner scanner = new Scanner(System.in);
    public static void main(String[] args) throws IOException {
        int testCases = 1;
        while (testCases-- > 0) {
            int k=scanner.nextInt();
            SinglyLinkedListNode []headList = new SinglyLinkedListNode[k];
            int p=0;
            for(int j=0;j<k;j++) {
                SinglyLinkedList llist = new SinglyLinkedList();
                int llistCount = scanner.nextInt();
                for (int i = 0; i < llistCount; i++) {
                    int llistItem = scanner.nextInt();
                    llist.insertNode(llistItem);
                }
                headList[p++] = llist.head;
            }
           printLinkedList(mergeKLists(headList));
        }
        scanner.close();
    }
}
