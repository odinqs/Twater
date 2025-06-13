# Twater
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Avatar, AvatarFallback, AvatarImage } from "@/components/ui/avatar";
import { Textarea } from "@/components/ui/textarea";
import { useState } from "react";
import { motion } from "framer-motion";

export default function TwaterDemo() {
  const [posts, setPosts] = useState([
    { id: 1, user: "yeşilpenguen", text: "Bugün gökyüzü çok güzel...", time: "2s" },
    { id: 2, user: "mavikarga", text: "Doğa her zaman kazanır.", time: "5s" },
  ]);
  const [newPost, setNewPost] = useState("");

  const handlePost = () => {
    if (newPost.trim() === "") return;
    const post = {
      id: Date.now(),
      user: "sen", // demo kullanıcı
      text: newPost,
      time: "şimdi",
    };
    setPosts([post, ...posts]);
    setNewPost("");
  };

  return (
    <div className="max-w-2xl mx-auto p-4 space-y-4">
      <motion.div initial={{ opacity: 0 }} animate={{ opacity: 1 }}>
        <Card className="bg-white rounded-2xl shadow p-4">
          <CardContent className="flex gap-4">
            <Avatar>
              <AvatarImage src="https://i.pravatar.cc/100" />
              <AvatarFallback>S</AvatarFallback>
            </Avatar>
            <Textarea
              value={newPost}
              onChange={(e) => setNewPost(e.target.value)}
              placeholder="Ne düşünüyorsun?"
              className="flex-1 resize-none"
            />
          </CardContent>
          <div className="flex justify-end px-6 pb-4">
            <Button onClick={handlePost} className="rounded-full">
              Gönder
            </Button>
          </div>
        </Card>
      </motion.div>

      <div className="space-y-3">
        {posts.map((post) => (
          <motion.div
            key={post.id}
            initial={{ opacity: 0, y: 10 }}
            animate={{ opacity: 1, y: 0 }}
          >
            <Card className="bg-blue-50 border border-blue-100 rounded-2xl shadow-sm">
              <CardContent className="p-4">
                <div className="flex items-center gap-3 mb-2">
                  <Avatar>
                    <AvatarImage src={`https://robohash.org/${post.user}.png?set=set5`} />
                    <AvatarFallback>{post.user.charAt(0).toUpperCase()}</AvatarFallback>
                  </Avatar>
                  <div className="text-sm font-semibold">{post.user}</div>
                  <div className="text-xs text-gray-500 ml-auto">{post.time}</div>
                </div>
                <div className="text-sm text-gray-800 whitespace-pre-line">{post.text}</div>
              </CardContent>
            </Card>
          </motion.div>
        ))}
      </div>
    </div>
  );
}
