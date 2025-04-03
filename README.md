import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Avatar } from "@/components/ui/avatar";
import { Tabs, TabsList, TabsTrigger, TabsContent } from "@/components/ui/tabs";
import { Heart, MessageCircle, Users, Globe } from "lucide-react";

export default function LinkUp() {
  const [status, setStatus] = useState("");
  const [posts, setPosts] = useState([]);
  const [communities, setCommunities] = useState(["Fãs de React", "Programadores", "Música" ]);

  const handlePost = () => {
    if (status.trim() !== "") {
      setPosts([{ text: status, likes: 0, comments: [] }, ...posts]);
      setStatus("");
    }
  };

  const likePost = (index) => {
    const newPosts = [...posts];
    newPosts[index].likes += 1;
    setPosts(newPosts);
  };

  return (
    <div className="max-w-3xl mx-auto p-4">
      <h1 className="text-3xl font-bold text-center mb-6">LinkUp</h1>
      <Tabs defaultValue="feed" className="w-full">
        <TabsList className="flex justify-around mb-4">
          <TabsTrigger value="feed"><Heart className="mr-2" />Feed</TabsTrigger>
          <TabsTrigger value="friends"><Users className="mr-2" />Amigos</TabsTrigger>
          <TabsTrigger value="messages"><MessageCircle className="mr-2" />Mensagens</TabsTrigger>
          <TabsTrigger value="communities"><Globe className="mr-2" />Comunidades</TabsTrigger>
        </TabsList>
        
        <TabsContent value="feed">
          <Card className="mb-4">
            <CardContent>
              <div className="flex items-center space-x-2 mb-2">
                <Avatar className="w-10 h-10" />
                <Input value={status} onChange={(e) => setStatus(e.target.value)} placeholder="O que você está pensando?" />
              </div>
              <Button onClick={handlePost}>Postar</Button>
            </CardContent>
          </Card>
          
          {posts.map((post, index) => (
            <Card key={index} className="mb-4">
              <CardContent>
                <p>{post.text}</p>
                <div className="flex items-center space-x-4 mt-2">
                  <Button variant="ghost" onClick={() => likePost(index)}>
                    <Heart className="w-4 h-4 mr-1" /> {post.likes}
                  </Button>
                  <Button variant="ghost">
                    <MessageCircle className="w-4 h-4 mr-1" /> Comentar
                  </Button>
                </div>
              </CardContent>
            </Card>
          ))}
        </TabsContent>
        
        <TabsContent value="friends">
          <p>Lista de amigos em construção...</p>
        </TabsContent>
        
        <TabsContent value="messages">
          <p>Mensagens em construção...</p>
        </TabsContent>
        
        <TabsContent value="communities">
          <p>Comunidades:</p>
          <ul className="list-disc pl-4">
            {communities.map((community, index) => (
              <li key={index}>{community}</li>
            ))}
          </ul>
        </TabsContent>
      </Tabs>
    </div>
  );
}
